<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ex7</title>
</head>
<body>
<script>

function validateCityName(city) {
  const regex = /^[A-Za-zÀ-ÿ\s-]{2,}$/;
  return regex.test(city.trim());
}

async function getWeather(city) {
  const apiKey = 'SUA_API_KEY_AQUI'; 
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(city)}&appid=${apiKey}&units=metric&lang=pt`;

  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error('Cidade não encontrada.');

    const data = await response.json();
    return data.main.temp;
  } catch (error) {
    throw new Error(`Erro ao obter dados: ${error.message}`);
  }
}

async function main() {
  const city = prompt('Digite o nome de uma cidade:');

  if (!validateCityName(city)) {
    alert('Por favor, digite um nome de cidade válido (somente letras, espaços ou traços).');
    return;
  }

  try {
    const temperature = await getWeather(city);
    alert(`A temperatura atual em ${city} é de ${temperature.toFixed(1)}°C.`);
  } catch (error) {
    alert(error.message);
  }
}

main();



</script>
</body>
</html>
