<script lang="ts">
  // this branch uses enum for clearer definitions
  enum googlePlace {
    "River North" = "River North",
    "River West" = "River West",
    "West Loop" = "West Loop",
    "South Loop" = "South Loop",
    "Streeterville" = "Streeterville",
    "New Eastside" = "New Eastside",
    "Printer's Row" = "Printer's Row",
  }


  interface ResiderNeighborhood {
    id: number;
    primary: googlePlace;
    alias?: string;
  }

  const neighborhoods: ResiderNeighborhood[] = [
    {
      id: 1,
      primary: googlePlace["River North"],
    },
    {
      id: 2,
      primary: googlePlace["River West"],
    },
    {
      id: 3,
      primary: googlePlace["West Loop"],
      alias: "Way West"
    },
    {
      id: 4,
      primary: googlePlace["South Loop"],
    },
    {
      id: 5,
      primary: googlePlace["Streeterville"],
    },
    {
      id: 6,
      primary: googlePlace["New Eastside"],
      alias: "Lakeshore East",
    },
    {
      id: 7,
      primary: googlePlace["Printer's Row"],
    },
  ];

  interface ResiderProperty {
    id: number;
    primary: googlePlace;
    secondary?: googlePlace;
    zipcode?: number[]
  }

  const properties: ResiderProperty[] = [
    {
      id: 1,
      primary: googlePlace["River North"],
      zipcode: [60661, 60662]
    },
    {
      id: 2,
      primary: googlePlace["River North"],
      secondary: googlePlace["Streeterville"],
      zipcode: [60663]
    },
    {
      id: 3,
      primary: googlePlace["New Eastside"],
      zipcode: [60664, 60665]
    },
    {
      id: 4,
      primary: googlePlace["Printer's Row"],
      secondary: googlePlace["South Loop"],
      zipcode: [60666]
    },
    {
      id: 5,
      primary: googlePlace["South Loop"],
      zipcode: [60667, 60668, 60669]
    },
    {
      id: 6,
      primary: googlePlace["West Loop"],
      zipcode: [60610]
    },
    {
      id: 7,
      primary: googlePlace["River West"],
    },
  ];

  // util to make googlePlace enum iteratable
  const googlePlaces = [];
  for (const place in googlePlace) {
    googlePlaces.push(place);
  }
  

  let searchText: string // binded to the input field
  let lastSearchedText: string = "" 
  let searchResults: ResiderProperty[] = [];

  function onClick() {
    searchResults = []; // clear search results from last search
    search(searchText) // invoke new search
    lastSearchedText = searchText // save search text to display in results
    searchText = "" // clear binded input value
  }

  function search(searchText) {
      
    // is it a valid google places neighborhood?
    if (googlePlaces.includes(searchText)) {
      // great! then find properties with matching primary neighborhood
      getPropertiesByGooglePlace(searchText);
    } else {
      // not a valid google places neighborhood?
      // then search for neighborhood alias instead
      let aliasMatch = neighborhoods.filter(
        (neighborhood) => neighborhood.alias === searchText
      );
      // if matching alias, then get the associated primary neighborhood (a valid google place)
      // and rerun getPropertiesByGooglePlaces() with that primary neighborhood
      if (aliasMatch.length > 0) {
        getPropertiesByGooglePlace(aliasMatch[0].primary);
      } 
    }

    function getPropertiesByGooglePlace(searchString: string) {
      let primaryMatches = properties.filter(
        (property) => property.primary == searchString
      );
      
      // and properties with matching secondary neighborhoods
      let secondaryMatches = properties.filter(
        (property) => property.secondary == searchString
      );
      
      // push them both to the result
      primaryMatches.forEach((property) => {
        searchResults.push(property);
      });
      secondaryMatches.forEach((property) => {
        searchResults.push(property);
      });
    }
  }
  


</script>

<main>
  
    

    <h3>Search for properties by <code>google places neighborhood</code>, or <code>neighborhood alias</code></h3>
  <input bind:value={searchText} placeholder="Search for properties by google places neighborhood, or neighborhood alias" class="input"/>
  <button on:click={onClick} class="btn">Search</button>

  

  {#if searchResults.length > 0}
  <h3>🏢 {searchResults.length} properties match "{lastSearchedText}"</h3>
  {:else}
  {#if lastSearchedText.length == 0}
        <h3>Beware: case sensitive! 💾</h3>
        {:else}
    <h3>0 properties matches "{lastSearchedText}". try again 🤨 (case-sensitive)</h3>
    {/if}
  {/if}

  <hr class="divider">
 <div class="databases">

    <div>
    
    <h3>Google Places</h3>
    <table>
      <tr>
        <th scope="row">placeName</th>
      </tr>
  
      {#each googlePlaces as place}
        <tr>
          <td>{place}</td>
        </tr>
      {/each}
    </table>
</div>
   
  
    <div >
        <h3>Neighborhoods</h3>
    <table>
      <tr>
        <th scope="row">id</th>
        <th scope="row">primary</th>
        <th scope="row">alias</th>
      </tr>
      {#each neighborhoods as neighborhood}
        <tr>
          <td>{neighborhood.id}</td>
          <td>{neighborhood.primary}</td>
          <td>{neighborhood.alias != undefined ? neighborhood.alias : ""}</td>
        </tr>
      {/each}
    </table>
    </div>
  
    <div >
        <h3>Properties</h3>
    <table>
      <tr>
        <th scope="row">id</th>
        <th scope="row">primary</th>
        <th scope="row">secondary</th>
      </tr>
      {#each properties as property}
        <tr class={searchResults.some(result => result.id == property.id) && "selected"}>
          <td>{property.id}</td>
          <td>{property.primary}</td>
          <td>{property.secondary != undefined ? property.secondary : ""}</td>
        </tr>
      {/each}
    </table>
    </div>
 </div>

 <hr class="divider">

 <h3>Notable searches</h3>
 <li>Lakeshore East - (an alias that returns "New Eastside)</li>
 <li>South Loop - returns 2 properties (1 based on it's secondary neighborhood!)</li>
 <li>Printer's Row - returns property 4 again! in a different search</li>
 <li>sdfasdff - returns nothing!</li>



</main>

<style>
  * {
    font-family: Open Sans;
  }

  .databases {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-evenly;
      align-content: flex-start;

  }

  .divider {
    border-top:1px solid #bbb
  }

  .input {
      width: 50%;
      height: 50px;
      font-size: 16px;
  }

  .btn {
    height: 50px;
    border: none;
    background-color: gb(190, 190, 190);
    font-weight: 400;
    border-radius: 10px;
    font-size: 16px;
    padding: 0 20px;
  }

  .btn:hover {
      transform: scale(0.9)
  }

  table {
    border-collapse: collapse;
    border: 2px solid rgb(200, 200, 200);
    letter-spacing: 1px;
    font-size: 0.8rem;
  }

  td,
  th {
    border: 1px solid rgb(190, 190, 190);
    padding: 10px 20px;
  }

  th {
    background-color: rgb(235, 235, 235);
  }

  td {
    text-align: center;
  }

  /* tr:nth-child(even) td {
    background-color: rgb(250, 250, 250);
  }

  tr:nth-child(odd) td {
    background-color: rgb(245, 245, 245);
  } */

  tr.selected {
    background-color: #3c4043 ;
    color: white ;
    font-weight: 700;
  }

</style>
