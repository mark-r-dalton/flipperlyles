const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');

const app = express();
app.use(bodyParser.json());

app.post('/webhook', async (req, res) => {
  const event = req.body;

  if (event.type === 'user_registered') {
    const userEmail = event.data.email;

    // Add user to contract
    try {
      await axios.post('https://api.piano.io/publisher/licensing/contractUser/create', {
        contract_id: 'TMZAC7WOU3F2',
        user_email: userEmail
      }, {
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer XJWhO9yCEHaqRha1dso9TyLuxjqzGAquVbaDH0d7'
        }
      });

      // Redeem contract for user
      await axios.post('https://api.piano.io/publisher/licensing/contract/redeem', {
        contract_id: 'TMZAC7WOU3F2',
        user_email: userEmail
      }, {
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer XJWhO9yCEHaqRha1dso9TyLuxjqzGAquVbaDH0d7'
        }
      });

      res.status(200).send('User added and contract redeemed');
    } catch (error) {
      console.error('Error adding user to contract:', error);
      res.status(500).send('Internal Server Error');
    }
  } else {
    res.status(400).send('Event type not supported');
  }
});

app.listen(3000, () => {
  console.log('Webhook server is running on port 3000');
});
