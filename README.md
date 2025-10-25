Exp 2:
// script.js
const greet = (name = "World") => `Hello, ${name}!`;
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);
console.log(greet(), doubled);

Exp 3:
<!DOCTYPE html>
<html><body>
  <button id="btn">Click Me</button>
  <p id="msg"></p>
  <script>
document.getElementById('btn').addEventListener('click', () => {
      document.getElementById('msg').innerText = "Button Clicked!";});
  </script></body></html>

Exp 4:
File se

Exp 5:
import React, { useState } from "react";
export default function App() {
  const [count, setCount] = useState(0);
  return (<div>
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>);}

Exp 6:
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
function Home() { return <h2>Home Page</h2>; }
function About() { return <h2>About Page</h2>; }
export default function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home/>} />
        <Route path="/about" element={<About/>} />
      </Routes></BrowserRouter>);}

Exp 7:
import React, { useState, useEffect } from "react";
export default function App() {
  const [time, setTime] = useState(new Date().toLocaleTimeString());
  useEffect(() => {
    const timer = setInterval(() => setTime(new Date().toLocaleTimeString()), 1000);
    return () => clearInterval(timer);
  }, []);
  return <h2>Current Time: {time}</h2>;
}

Exp 8:
const express = require('express');
const app = express();
app.use(express.json());
let users = [{ id: 1, name: "theet" }];
app.get('/users', (req, res) => res.json(users));
app.post('/users', (req, res) => { users.push(req.body); res.json(users); });
app.put('/users/:id', (req, res) => {
  const id = +req.params.id;
  users = users.map(u => u.id === id ? req.body : u);
  res.json(users);
});
app.delete('/users/:id', (req, res) => {
  users = users.filter(u => u.id != req.params.id);
  res.json(users);
});
app.listen(3000, () => console.log("Server running on 3000"));

Exp 9:
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();
app.use(express.json());
const SECRET = "secret123";
app.post('/login', (req, res) => {
  const { username } = req.body;
  const token = jwt.sign({ username }, SECRET, { expiresIn: '1h' });
  res.json({ token });
});
app.get('/protected', (req, res) => {
  const auth = req.headers.authorization?.split(" ")[1];
  try {
    const decoded = jwt.verify(auth, SECRET);
    res.json({ message: "Welcome " + decoded.username });
  } catch {
    res.status(401).json({ error: "Invalid token" });
  }
});
app.listen(4000, () => console.log("Auth API on 4000"));
Run
Use thunder client →
POST /login with { "username": "any username" }

Copy token → GET /protected with header Authorization: Bearer <token>

Exp 10:
const express = require('express');
const mongoose = require('mongoose');
const app = express();
app.use(express.json());
mongoose.connect('mongodb://localhost:27017/testdb');
const User = mongoose.model('User', new mongoose.Schema({ name: String }));
app.post('/users', async (req, res) => res.json(await User.create(req.body)));
app.get('/users', async (req, res) => res.json(await User.find()));
app.put('/users/:id', async (req, res) => res.json(await User.findByIdAndUpdate(req.params.id, req.body, { new: true })));
app.delete('/users/:id', async (req, res) => res.json(await User.findByIdAndDelete(req.params.id)));
app.listen(5000, () => console.log('Mongo API running on 5000'));

<img width="451" height="686" alt="image" src="https://github.com/user-attachments/assets/764ded40-da69-44ea-8c4f-2d5e13216972" />
