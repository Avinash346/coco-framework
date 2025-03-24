# Assignment Solutions

# Section 1: Aptitude &amp; Logical Reasoning (20 marks)

## 1. A train running at 60 km/h crosses a pole in 9 seconds. Find the length of the train. (4 marks)

_1. Convert the speed to meters per second:_

_Speed = 60 km/h\
To convert km/h to m/s, multiply by 5/18.\
Speed = 60 * (5/18) m/s\
Speed = (300/18) m/s\
Speed = (50/3) m/s\
2. Calculate the length of the train:_\

When a train crosses a pole, the distance covered is equal to the length of the train.\
Distance = Speed * Time\
Length of the train = (50/3) m/s * 9 s\
Length of the train = (50 * 9) / 3 m\
Length of the train = 450 / 3 m\
Length of the train = 150 m\
Therefore, the length of the train is 150 meters.\

## 2. If A is twice as good a workman as B, and together they finish a job in 18 days, how long would it take A alone? (4 marks)

Let A's one-day work be 'a'\
Let B's one-day work be 'b'\
A is twice as good as B: a = 2b\
Together they finish the job in 18 days: 18(a + b) = 1 (where 1 represents the whole job)\
Substitute 'a = 2b' into the second equation: 18(2b + b) = 1\
Simplify: 18(3b) = 1\
54b = 1\
b = 1/54 (This is B's one-day work)\
Now, find A's one-day work: a = 2b = 2 * (1/54) = 2/54 = 1/27 (This is A's one-day work)\
If A does 1/27 of the job in one day, then A takes 27 days to complete the entire job.\
Therefore, A alone would take 27 days to finish the job.

## 3. Find the missing number in the series: 2, 6, 12, 20, 30, ? (4 marks)

missing number is 42

## 4. A sum of money is divided among A, B, and C in the ratio 3:5:7. If C gets INR 4200, find the
total sum. (4 marks)

If C's share (7 parts) is INR 4200, then one part is INR 600. The total ratio parts are 3+5+7=15, so the total sum is 15 * INR 600 = INR 9000.

## 5. If the letters of the word &#39;QUODROID&#39; are arranged randomly, what is the probability that it starts with &#39;Q&#39;? (4 marks)

the probability that the word 'QUODROID' starts with 'Q' is 1/8.

# Section 2: Technical MCQs (30 marks)

 ## 1. Which of the following is NOT a characteristic of a relational database? (6 marks)\
a) ACID Compliance\
b) Stored Procedures\
c) Non-structured schema\
d) Foreign Keys
Ans- c

## 2. In Node.js, which module is used to create a server? (6 marks)\
a) fs\
b) http\
c) express\
d) path\
Ans-b

## 3. What is the correct way to fetch data in React using hooks? (6 marks)\
a) useState(fetch(&#39;api/data&#39;))\
b) useEffect(() =&gt; fetchData(), [])\
c) useMemo(() =&gt; fetchData(), [])\
d) useReducer(fetchData, [])\
Ans-b

## 4. In Express.js, which method is used to handle POST requests? (6 marks)\
a) app.get()\
b) app.post()\
c) app.put()\
d) app.delete()\
Ans-b

## 5. Which HTTP method is not idempotent? (6 marks)\
a) GET\
b) POST\
c) DELETE\
d) PUT\
Ans-b

# Section 3: Coding Problems (50 marks)

## 1. Node.js/Express.js: (20 marks) Write an Express.js route that accepts a POST request with a JSON payload containing a list of numbers. The function should return the sum of all even numbers in the list.Input: { &quot;numbers&quot;: [1, 2, 3, 4, 5, 6] } Output: { &quot;sum&quot;: 12 }

``` javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

app.post('/sumEven', (req, res) => {
  const numbers = req.body.numbers;

  if (!Array.isArray(numbers)) {
    return res.status(400).json({ error: 'Input must be an array of numbers' });
  }

  let sum = 0;
  for (const num of numbers) {
    if (typeof num !== 'number') {
      return res.status(400).json({error: 'Array contains non-number value'});
    }
    if (num % 2 === 0) {
      sum += num;
    }
  }

  res.json({ sum });
});

app.listen(port, () => {
  console.log(`Server listening at ${port}`);
});
```
## 2. SQL: (10 marks) Write a SQL query to find all users who have placed at least two orders in the last month. Tables: Users (id, name, email) Orders (id, user_id, order_date, amount)

 ``` sql
 SELECT u.id, u.name, u.email
FROM Users u
JOIN Orders o ON u.id = o.user_id
WHERE o.order_date >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH)
GROUP BY u.id, u.name, u.email
HAVING COUNT(o.id) >= 2;
```

## 3. React/Next.js: (20 marks) Create a simple React functional component that fetches a list of users from an API and displays them in a list. Include error handling.

``` javascript
import { useEffect, useState } from "react";

export default function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const response = await fetch("api end point");
        if (!response.ok) {
          throw new Error("Failed to fetch users");
        }
        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchUsers();
  }, []);

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h2>User List</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name} - {user.email}</li>
        ))}
      </ul>
    </div>
  );
}
```




