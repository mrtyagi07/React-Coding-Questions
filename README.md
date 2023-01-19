# React-Coding-Questions


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
        </table>
      </div>
    </div>
  );
}


```
