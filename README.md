# React Interview Coding Questions & Answers

> Click :star:if you like the project and follow [@mrtyagi07](https://twitter.com/mrtyagi07) for more updates.
---

<p align="center">
  <a href=https://twitter.com/mrtyagi07>
    <img src="https://i.ibb.co/ZLpJXrY/vaibhav-tyagi-logo-removebg-preview.png" alt="Vaibhav's Logo">
  </a>
  <p align="center">
    Explore the best <a href=https://vaibhavtyagi.hashnode.dev/ target="_blank">blogs</a> to learn JavaScript and React.
  </p>
</p>

---



### 1) Create a React component that renders a list of items from an array of data, and allows the user to filter the list by a search term.

 <b>Solution ➡️</b>

   ``` js
//App.js
      
import React, { useState } from "react";

export default function App() {
  const items = [
    {
      id: 1,
      name: "item1",
      category: "category1",
    },
    {
      id: 2,
      name: "item2",
      category: "category2",
    },
    {
      id: 3,
      name: "item3",
      category: "category1",
    },
    {
      id: 4,
      name: "item4",
      category: "category3",
    },
    {
      id: 5,
      name: "item5",
      category: "category2",
    },
  ];

  const [search, setSearch] = useState(items);
  const [find, setFind] = useState("");

  function handleSearch() {
    if (find === "") {
      setSearch(items);
    } else {
      setSearch(
        items.filter(
          (item) => item.name.includes(find) || item.category.includes(find),
        ),
      );
    }
  }

  function handleClear() {
    setFind("");
    setSearch(items);
  }

  return (
    <div className="App">
      <h1>React Coding Questions</h1>
      <h2>Happy Coding!</h2>
      <div>
        <input
          type="text"
          placeholder="Enter search term"
          value={find}
          onChange={(e) => setFind(e.target.value)}
        />
        <button onClick={handleSearch}>Search</button>
        <button onClick={handleClear}>Clear</button>
        {search.map((item) => (
          <div key={item.id}>
            <p>Name: {item.name}</p>
            <p>Category: {item.category}</p>
          </div>
        ))}
      </div>
    </div>
  );
}


   ```
   
### 2) Create a React component that renders a form with two input fields (username and password) and a submit button. The form should validate the input fields and display error messages if the input is not valid. The form should also handle the form submission and display a success message if the input is valid.

Solution ➡️

``` js
import "./styles.css";
import React, { useState } from "react";


export default function App() {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    console.log(username, password);
    if (username === "Vaibhav" && password === "12345")
      alert("Form is submitted!");
    else alert("Form is not submitted!");
    setUsername("");
    setPassword("");
  }

  return (
    <div className="App">
      <h1>React Coding Questions</h1>
      <h2>Happy Coding!</h2>
      <div>
        <form onSubmit={handleSubmit}>
          <input
            type="text"
            placeholder="Enter username"
            onChange={(e) => setUsername(e.target.value)}
          />
          <input
            type="password"
            placeholder="Enter password"
            onChange={(e) => setPassword(e.target.value)}
          />
          <button type="submit">Submit</button>
        </form>
      </div>
    </div>
  );
}

```

### 3) Create a React component that renders a table with a list of employees. Each row should display the employee's name, age, and salary. The table should also have a search input that filters the list of employees by name. Also, it should have a button to sort the list of employees by salary in ascending or descending order.

Solution ➡️

``` js
import "./styles.css";
import React, { useState } from "react";

export default function App() {
  const [value, setValue] = useState("");
  const data = [
    {
      id: 1,
      name: "Vaibhav",
      age: "22",
      salary: 10
    },
    {
      id: 2,
      name: "Jay",
      age: "25",
      salary: 15
    },
    {
      id: 3,
      name: "Pooja",
      age: "18",
      salary: 5
    },
    {
      id: 4,
      name: "Pushpa",
      age: "30",
      salary: 23
    },
    {
      id: 5,
      name: "Rocky",
      age: "50",
      salary: 90
    }
  ];
  const [search, setSearch] = useState(data);

  function handleSubmit(e) {
    e.preventDefault();
    console.log(value);
    setSearch(data.filter((el) => el.name.includes(value)));
  }

  function sort(e) {
    e.preventDefault();
    const selectedOption = e.target.value;
    if (selectedOption === "Ascending") {
      setSearch(data.sort((a, b) => a.salary - b.salary));
    } else if (selectedOption === "Descending") {
      setSearch(data.sort((a, b) => b.salary - a.salary));
    } else {
      setSearch(data);
    }
  }

  return (
    <div className="App">
      <h1>React Coding Questions</h1>
      <h2>Happy Coding!</h2>
      <div>
        <input
          type="text"
          onChange={(e) => setValue(e.target.value)}
          placeholder="Enter name"
        />
        <button type="button" onClick={handleSubmit}>
          Serach
        </button>
        <select onChange={(e) => sort(e)}>
          <option>Default</option>
          <option>Ascending</option>
          <option>Descending</option>
        </select>
        <table>
          <tbody>
            <tr>
              <th>Name</th>
              <th>Age</th>
              <th>salary</th>
            </tr>
            {search.length <= 0
              ? "No data Found!😔"
              : search.map((el) => (
                  <tr key={el.id}>
                    <td>{el.name}</td>
                    <td>{el.age}</td>
                    <td>{el.salary}</td>
                  </tr>
                ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}



```

### 4) Create a React component that displays a list of movies from the Open Movie Database (OMDB) API (http://www.omdbapi.com/). The component should have a search input that allows users to search for movies by title and a button to trigger the search. The component should also display the title, year, and poster of each movie in the list. Finally, the component should include error handling for when the API request fails. (You can use the API key apikey=yourkey to make the request).

Solution ➡️

``` js
import "./styles.css";
import React, { useEffect, useState } from "react";

export default function App() {
  const [search, setSearch] = useState("");
  const [data, setData] = useState({});

  const handleSearch = async () => {
    try {
      const response = await fetch(
        `https://www.omdbapi.com/?t=${search}&apikey=7fe42f18`
      );
      const movieData = await response.json();
      console.log(movieData);
      setData(movieData);
    } catch (err) {
      console.log(err);
    }
  };

  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
      <input
        type="text"
        placeholder="Enter Movie Name"
        onChange={(e) => setSearch(e.target.value)}
      />
      <button type="button" onClick={handleSearch}>
        Search
      </button>
      {/* //title, year, and poster */}

      <div className="card">
        {Object.keys(data).length <= 0 ? (
          <p>"No data found! 😔"</p>
        ) : (
          <>
            <img src={data?.Poster} alt="postar" />
            <div class="container">
              <h4>
                <b>{data?.Title}</b>
              </h4>
              <p>{data?.Year}</p>
            </div>
          </>
        )}
      </div>
    </div>
  );
}

```

### 4) Create a React component that displays a list of airlines image and name from the Fake Rest API (https://www.instantwebtools.net/fake-rest-api#read-airlines/). Component should display a list of airlines from a given API, with the ability to change the number of items displayed per page and navigate through the pages of the list? Finally, the component should include error handling for when the API request fails.

Solution ➡️

- CodeSand Box https://codesandbox.io/s/airlines-trh6sl?file=/src/App.js

``` js
import "./styles.css";
import React, { useEffect, useState } from "react";

export default function App() {
  const [airlines, setAirlines] = useState([]);
  const [page, setPage] = useState(0);
  const [size, setSize] = useState(10);

  useEffect(() => {
    fetch(
      `https://api.instantwebtools.net/v1/passenger?page=${page}&size=${size}`
    )
      .then((res) => res.json())
      .then((data) => setAirlines(data.data))
      .catch((err) => console.log(err));
  }, [page, size]);

  const handlePageChange = (increment) => {
    setPage(page + increment);
  }

  return (
    <div className="App">
      <h1>React Coding Questions</h1>
      <h2>Happy Coding!</h2>
      {airlines?.map((el) => (
        <div key={el._id} className="wrapper">
          <img src={el.airline[0].logo} alt="airline" />
          <h1>{el.airline[0].name}</h1>
        </div>
      ))}
      <div className="pagination">
        <button onClick={() => handlePageChange(-1)}>&laquo;</button>
        <button onClick={() => handlePageChange(1)}>&raquo;</button>
      </div>

      <label htmlFor="size">
        Want to see more items in one page? (Write a number):
      </label>

      <input
        type="number"
        required
        onChange={(e) => setSize(e.target.value)}
        value={size}
      />
    </div>
  );
}


```

### 3) Create a React component that allows users to search for GIFs using the Giphy API. The component should have an input field for the search query and a button to initiate the search. When the search button is clicked, the component should make a GET request to the Giphy API and display the results in a grid of GIFs. The component should also handle any errors that occur during the API request and display an appropriate error message. The Giphy API (https://developers.giphy.com/)

Solution ➡️

``` js
import React, { useState } from "react";

import "./app.css";

const App = () => {
  const [input, setInput] = useState("");
  const [data, setData] = useState([]);

  const handleSearch = () => {
    fetch(
      `https://api.giphy.com/v1/gifs/search?api_key=YOUR_KEY&q=${input}&limit=25&offset=0&rating=g&lang=en`
    )
      .then((res) => res.json())
      .then((data) => setData(data.data))
      .catch((err) => console.log(err));
  };

  return (
    <>
      <div className="flex justify-center items-center p-8">
        <div className="flex items-center border-b border-teal-500 py-2">
          <input
            className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
            type="text"
            placeholder="LOL"
            aria-label="gif"
            value={input}
            onChange={(e) => setInput(e.target.value)}
          />
          <button
            className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
            type="button"
            onClick={handleSearch}
          >
            Search
          </button>
        </div>
      </div>

      <div className="grid grid-cols-3 gap-4">
        {data?.map((el) => (
          <div
            key={el.id}
            className="max-w-sm rounded overflow-hidden shadow-lg"
          >
            <img
              className="w-full"
              src={el.images.original.url}
              alt="Gify"
            />
          </div>
        ))}
      </div>
    </>
  );
};

export default App;

https://codesandbox.io/s/gify-question-nh03k7


```

### 4) Create a React component that renders a table with a list of users. Each row in the table should display the user's first name, last name, and email address. The component should have a text input that allows the user to filter the list of users by their first name. Use the following API to fetch the list of users: https://jsonplaceholder.typicode.com/users.

Solution ➡️

``` js
import React, { useEffect, useState } from "react";

import "./app.css";

const App = () => {
  const [data, setData] = useState([]);
  const [input, setInput] = useState("");

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setData(data))
      .catch((err) => console.log(err));
  }, [input]);

  const handleSearch = () => {
    const string = input.charAt(0).toUpperCase() + input.slice(1);
    setData(
      data.filter(
        (el) =>
          el.name.includes(string) ||
          el.username.includes(string) ||
          el.email.includes(string)
      )
    );
  };

  return (
    <div className="w-full h-screen p-8">
      <div className="flex items-center border-b border-teal-500 py-2 mb-8">
        <input
          className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="Vaibhav"
          value={input}
          onChange={(e) => setInput(e.target.value)}
        />
        <button
          className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
          type="button"
          onClick={handleSearch}
        >
          Search
        </button>
      </div>
      <div className="relative overflow-x-auto">
        <table className="w-full text-sm text-left text-gray-500 ">
          <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 ">
            <tr>
              <th scope="col" className="px-6 py-3">
                Name
              </th>
              <th scope="col" className="px-6 py-3">
                Username
              </th>
              <th scope="col" className="px-6 py-3">
                Email
              </th>
            </tr>
          </thead>
          <tbody>
            {data.map((el) => (
              <tr
                key={el.id}
                className="bg-white border-b dark:bg-gray-800 dark:border-gray-700"
              >
                <td className="px-6 py-4">{el.name}</td>
                <td className="px-6 py-4">{el.username}</td>
                <td className="px-6 py-4">{el.email}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};

export default App;

```
https://codesandbox.io/s/users-api-77g76l?file=/src/app.jsx
