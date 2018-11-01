# catalyst-weather-app

## Link to Live Project:

[Deployed link](https://google.com)

### Project setup
```
npm install
```

_In your src folder, create a lib folder and inside that, make an API.js file. Inside that file, paste in_

```javascript
const API_KEY = 'YOUR SECRET API KEY YOU GET WHEN YOU SIGN UP FOR A KEY';

function getCoordinatesFromCityName(location) {
    return fetch(`https://api.openweathermap.org/data/2.5/find?q=${location}&type=like&units=imperial&appid=${API_KEY}`)
    .then(response => response.json());
}

function getForecast(lat=39.7392, lng=-104.9848) {
    return fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${lat}&lon=${lng}&units=imperial&appid=${API_KEY}`)
        .then(response => response.json());
}


export default {
    getCoordinatesFromCityName,
    getForecast
};
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```


