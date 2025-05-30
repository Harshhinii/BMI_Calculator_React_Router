# Ex06 BMI Calculator
## Date: 30-05-2025

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM

app.js
```
import React, { useState } from 'react';
import './App.css';

function App() {
  const [weight, setWeight] = useState('');
  const [height, setHeight] = useState('');
  const [gender, setGender] = useState('');
  const [bmi, setBmi] = useState(null);
  const [message, setMessage] = useState('');

  const calculateBMI = (e) => {
    e.preventDefault();

    if (!weight || !height || weight <= 0 || height <= 0 || !gender) {
      setMessage("Please fill all fields with valid values.");
      setBmi(null);
      return;
    }

    const heightInMeters = height / 100;
    const bmiValue = (weight / (heightInMeters * heightInMeters)).toFixed(2);
    setBmi(bmiValue);

    if (bmiValue < 18.5) {
      setMessage("Underweight");
    } else if (bmiValue >= 18.5 && bmiValue < 24.9) {
      setMessage("Normal weight");
    } else if (bmiValue >= 25 && bmiValue < 29.9) {
      setMessage("Overweight");
    } else {
      setMessage("Obese");
    }
  };

  const reset = () => {
    setWeight('');
    setHeight('');
    setGender('');
    setBmi(null);
    setMessage('');
  };

  return (
    <div className="bmi-container">
      <h1>BMI Calculator</h1>
      <form onSubmit={calculateBMI}>
        <div className="input-group">
          <label>Gender:</label>
          <select value={gender} onChange={(e) => setGender(e.target.value)}>
            <option value="">-- Select Gender --</option>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
          </select>
        </div>

        <div className="input-group">
          <label>Weight (kg):</label>
          <input
            type="number"
            value={weight}
            onChange={(e) => setWeight(e.target.value)}
            placeholder="e.g. 70"
          />
        </div>

        <div className="input-group">
          <label>Height (cm):</label>
          <input
            type="number"
            value={height}
            onChange={(e) => setHeight(e.target.value)}
            placeholder="e.g. 170"
          />
        </div>

        <button type="submit">Calculate</button>
        <button type="button" className="reset" onClick={reset}>Reset</button>
      </form>

      {bmi && (
        <div className="result">
          <h2>Your BMI is: {bmi}</h2>
          <p>Gender: {gender}</p>
          <p>Status: {message}</p>
        </div>
      )}
    </div>
  );
}

export default App;
```
app.css

```
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: #639ac7;
}

.bmi-container {
  max-width: 400px;
  margin: 60px auto;
  padding: 30px;
  background: rgb(27, 106, 152);
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0,0,0,0.1);
  text-align: center;
}

h1 {
  color: #333;
}

.input-group {
  margin: 20px 0;
  text-align: left;
}

.input-group label {
  display: block;
  font-weight: 600;
  margin-bottom: 5px;
}

.input-group select,
.input-group input {
  width: 100%;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ccc;
}


button {
  padding: 10px 20px;
  margin: 10px 5px;
  border: none;
  background-color: #4CAF50;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}

button.reset {
  background-color: #c711b4;
}

.result {
  margin-top: 30px;
}

.result h2 {
  color: #4CAF50;
}

.result p {
  font-weight: bold;
}
```


## OUTPUT

![image](https://github.com/user-attachments/assets/b421ee43-4cd5-46d5-9254-4da5652d8462)

![image](https://github.com/user-attachments/assets/bd67417f-085b-4209-b2a7-6b8996ca8d05)





## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
