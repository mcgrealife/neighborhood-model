<script lang="ts">

    interface googlePlace {
        name: String;
        placeId: String;
    }

    const places = {
        "River North": "ChIJS2Sm7bUsDogR96Ftwh",
        "River West": "ChIJ6XSSwtIsDogR5xHPvcHH9r0"
    }

    console.log(places["River North"])

    const googlePlaces: googlePlace[] = [
      {
        "name": "River North",
        "placeId":"ChIJS2Sm7bUsDogR96Ftwh-QLis"
      },
      {
        "name": "River West",
        "placeId": "ChIJ6XSSwtIsDogR5xHPvcHH9r0"
      },
      {
        "name": "West Loop",
        "placeId": "ChIJ3baIM9osDogRVpFwiwqSLJQ"
      },
      {
        "name": "South Loop",
        "placeId": "ChIJ-xi8O48sDogRcBMK7WhN4pE"
        },
      {
        "name": "Streeterville",
        "placeId": "ChIJ0UDWv6osDogRr7DEnYYPr4Y"
      },
      {
        "name": "New Eastside",
        "placeId": "ChIJjXp9wFcrDogRru8nq-MsgWY"
      },
      {
        "name": "Printer's Row",
        "placeId": "ChIJHyxSl5csDogRcG_kdoAw_ZE"
        }
    ]

    console.log(googlePlaces.filter(place =>
        place.name == "River North"
    ))
    
    interface ResiderNeighborhood {
      id: number;
      primary: googlePlace;
      alias?: string;
    }
    
    const neighborhoods: ResiderNeighborhood[] = [
      {
        id: 1,
        primary: "River North",
        alias: ""
      },
       {
        id: 2,
        primary: "River West",
        alias: ""
      },
       {
        id: 3,
        primary: "West Loop",
        alias: ""
      },
       {
        id: 4,
        primary: "South Loop",
        alias: ""
      },
       {
        id: 5,
        primary: "Streeterville",
        alias: ""
      },
       {
        id: 6,
        primary: "New Eastside",
        alias: "Lakeshore East"
      },
       {
        id: 7,
        primary: "Printer's Row",
        alias: ""
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
        primary: googlePlaces[0]
      },
      {
        id: 2,
        primary: "River North",
      },
      {
        id: 3,
        primary: "New Eastside",
      },
      {
        id: 4,
        primary: "Printer's Row",
        secondary: "South Loop"
      },
      {
        id: 5,
        primary: "South Loop",
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
      {#each googlePlaces as place}
        <tr>
          <td>{place.name}</td>
          <td>{place.placeId}</td>
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
    