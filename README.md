jsx
// client/src/containers/HackathonList.js
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const HackathonList = () => {
  const [hackathons, setHackathons] = useState([]);

  useEffect(() => {
    axios.get('/api/hackathons')
      .then(response => {
        setHackathons(response.data);
      })
      .catch(error => {
        console.error(error);
      });
  }, []);

  return (
    <div>
      <h1>Hackathons</h1>
      <ul>
        {hackathons.map(hackathon => (
          <li key={hackathon.id}>
            <Link to={`/hackathons/${hackathon.id}`}>
              {hackathon.name}
            </Link>
          </li>
        ))}
      </ul>
    </div>
  );
};

export default HackathonList;

And here's a sample code snippet for the hackathons route:

// server/routes/hackathons.js
const express = require('express');
const router = express.Router();
const Hackathon = require('../models/Hackathon');

router.get('/', async (req, res) => {
  try {
    const hackathons = await Hackathon.find();
    res.json(hackathons);
  } catch (error) {
    console.error(error);
    res.status(500).json({ message: 'Error fetching hackathons' });
  }
});

module.exports = router;

