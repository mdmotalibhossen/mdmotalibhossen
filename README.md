-const express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

let transactions = [];

app.post('/addTransaction', (req, res) => {
  const { amount, nationalID } = req.body;

  if (nationalID.length === 13) {
    const dividend = amount * 0.20;
    const transaction = { amount, dividend, nationalID };
    transactions.push(transaction);
    res.status(200).json(transaction);
  } else {
    res.status(400).json({ error: 'অবৈধ জাতীয় আইডি!' });
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
