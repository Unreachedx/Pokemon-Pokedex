Pokémon Fetcher
A simple web application that fetches and displays a list of the first 150 Pokémon using the PokeAPI. The application fetches Pokémon data, including their name, image, ID, and type, and displays them in a styled list.

Features
Fetches data for the first 150 Pokémon from the PokeAPI.
Displays Pokémon names, images, IDs, and types.
Dynamically updates the webpage with the Pokémon data.
Technologies Used
HTML
CSS
JavaScript (Vanilla)
How It Works
The application fetches data for the first 150 Pokémon by making API calls to https://pokeapi.co/api/v2/pokemon/{id}, where {id} is the Pokémon's unique ID.
It uses Promise.all to wait for all fetch requests to complete before processing the results.
Each Pokémon's data is formatted (name, id, image, and type) and displayed in a card format.
The results are dynamically inserted into the DOM inside an unordered list (<ul id="pokedex">).

Installation and Usage
Clone the repository:


git clone <repository-url>
Open the index.html file in a browser.

You should see a list of Pokémon displayed with their names, images, IDs, and types.

Code Explanation
Fetching Pokémon Data: The fetchPokemon function makes asynchronous requests to the PokeAPI for each Pokémon (IDs 1–150). The results are processed and passed to the displayPokemon function.

Displaying Pokémon: The displayPokemon function formats the Pokémon data into HTML and appends it to the #pokedex container.

CSS Styling: The Pokémon are styled using CSS to display their images and details in a clean, card-like layout.

Example
js
const fetchPokemon = () => {
  const promises = [];
  for (let i = 1; i <= 150; i++) {
    const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
    promises.push(fetch(url).then((res) => res.json()));
  }

  Promise.all(promises).then((results) => {
    const pokemon = results.map((data) => ({
      name: data.name,
      id: data.id,
      image: data.sprites['front_default'],
      type: data.types.map((type) => type.type.name).join(', '),
    }));
    displayPokemon(pokemon);
  });
};

const displayPokemon = (pokemon) => {
  const pokemonHTMLString = pokemon
    .map(
      (pokeman) => `
        <li class="card">
            <img class="card-image" src="${pokeman.image}" />
            <h2 class="card-title">${pokeman.id}. ${pokeman.name}</h2>
            <p class="card-subtitle">Type: ${pokeman.type}</p>
        </li>`
    )
    .join('');
  document.getElementById('pokedex').innerHTML = pokemonHTMLString;
};


License
This project is licensed under the MIT License.
