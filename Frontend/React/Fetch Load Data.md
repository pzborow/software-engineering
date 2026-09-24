# Fetch Load Data

```.javascript
import "./styles.css";
import React, {useEffect, useState} from "react";
import axios from 'axios';
export default function App() {
  const [isLoading, setIsLoading] = useState(false);
  const [isError, setIsError] = useState(false);
  const [userData, setUserData] = useState(null);
  useEffect(() => {
    async function getUserData() {
      try {
        setIsLoading(true);
        const {data} = await axios.get(`https://jsonplaceholder.typicode.com/users/1`);
        setUserData(data);
        setIsLoading(false);
      } catch (error) {
        setIsLoading(false);
        setIsError(error);
      }
    }
    getUserData();
  }, []);
  return (
    <div>
      {isLoading && (<div> ...Loading </div>)}
      {isError && (<div>An error occured: {isError.message}</div>)}
      {userData && (<div>The username is : {userData.username}</div>)}
    </div>
  )
}
```

[Bardziej elegancko](https://blog.logrocket.com/whats-new-in-react-query-3/)