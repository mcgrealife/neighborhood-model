<script lang="ts">

 // these are valid google places
    enum googlePlace {
        "River North"="River North",
        "River West"= "River West",
        "West Loop" = "West Loop",
        "South Loop" = "South Loop",
        "Streeterville" = "Streeterville",
        "New Eastside" = "New Eastside",
        "Printer's Row" = "Printer's Row"
    }

    // enum googlePlace {
    //     "River North" = "ChIJS2Sm7bUsDogR96Ftwh-QLis",
    //     "River West" = "ChIJ6XSSwtIsDogR5xHPvcHH9r0",
    //     "West Loop" = "ChIJ3baIM9osDogRVpFwiwqSLJQ",
    //     "South Loop" = "ChIJ-xi8O48sDogRcBMK7WhN4pE",
    //     "Streeterville" = "ChIJ0UDWv6osDogRr7DEnYYPr4Y",
    //     "New Eastside" ="ChIJjXp9wFcrDogRru8nq-MsgWY",
    //     "Printer's Row" ="ChIJHyxSl5csDogRcG_kdoAw_ZE"
    // }

    
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
      },
       {
        id: 7,
        primary: googlePlace["Printer's Row"],
      }
    ]
    
    interface ResiderProperty {
      id: number;
      primary: googlePlace;
      secondary?: googlePlace;
    }
    
    const properties: ResiderProperty[] = [
      {
        id: 1,
        primary: googlePlace["River North"]
      },
      {
        id: 2,
        primary: googlePlace["River North"]
      },
      {
        id: 3,
        primary: googlePlace["New Eastside"],
      },
      {
        id: 4,
        primary: googlePlace["Printer's Row"],
        secondary: googlePlace["South Loop"]
      },
      {
        id: 5,
        primary: googlePlace["South Loop"],
      }    
    ]
    
    let searchText
    
    function search() {
      console.log(searchText)
    
    }
    
    </script>
    
    <input bind:value={searchText} placeholder="filter by neighborhood">
    <button on:click={search}>Search</button>


    
    
    <h3>Google Places</h3>  
    <table>
      <tr>
        <th scope="row">placeName</th>
        <th scope="row">placeId</th>
      </tr>
      {#each googlePlace as place}
        <tr>
          <td>{place}</td>
          <td>{place.value}</td>
        </tr>
      {/each}
    </table>
    
    
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
          <td>{neighborhood.alias}</td>
        </tr>
      {/each}
    </table>
    
    <h3>Properties</h3>  
    <table>
      <tr>
        <th scope="row">id</th>
        <th scope="row">primary</th>
        <th scope="row">secondary</th>
      </tr>
      {#each properties as property}
        <tr>
          <td>{property.id}</td>
          <td>{property.primary}</td>
          <td>{property.secondary}</td>
        </tr>
      {/each}
    </table>
    
    
    <style>
      * {
        font-family: Open Sans;
      }
    
      table {
      border-collapse: collapse;
      border: 2px solid rgb(200,200,200);
      letter-spacing: 1px;
      font-size: 0.8rem;
    }
    
    td, th {
      border: 1px solid rgb(190,190,190);
      padding: 10px 20px;
    }
    
    th {
      background-color: rgb(235,235,235);
    }
    
    td {
      text-align: center;
    }
    
    tr:nth-child(even) td {
      background-color: rgb(250,250,250);
    }
    
    tr:nth-child(odd) td {
      background-color: rgb(245,245,245);
    }
    
    
    </style>
    