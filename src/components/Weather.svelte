<script lang="ts">
  import ErrorAlert from "./ErrorAlert.svelte"
  import Loading from "./Loading.svelte"
  import SearchForm from "./SearchForm.svelte"
  import WeatherData from "./WeatherData.svelte"
  import type { WeaterDataInterface } from "../interfaces/Weather"

  const KEY = "3bbee421699100ea34422cb81d8c1dc3"

  const getWeatherData = async (city: string = "Lima") => {
    if (city.trim() === "") throw new Error("City is required")
    const baseURL = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${KEY}`
    const res: Response = await fetch(baseURL)

    if (!res.ok) throw new Error("This place could not found")

    const data: WeaterDataInterface = await res.json()

    return data
  }

  let promise = getWeatherData()

  const handleSubmit = (e: any) => {
    promise = getWeatherData(e.detail)
  }
</script>

<div class="container">
  <div class="row">
    <div class="col-12">
      <SearchForm on:handleSubmit={handleSubmit} />
    </div>
    {#await promise}
      <div class="col-12">
        <Loading />
      </div>
    {:then weather}
      <WeatherData {weather} />
    {:catch error}
      <ErrorAlert {error} />
    {/await}
  </div>
</div>
