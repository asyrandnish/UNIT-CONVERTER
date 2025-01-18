<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ENGINEERING UNIT CONVERTER</title>
    <style>
body    {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #87CEEB; /* Sky blue background */
        }

h1      {
            text-align: center;
            color: white;
            background-color: #0077BE; /* Ocean blue for the header */
            padding: 10px;
            border-radius: 8px;
            max-width: 600px; /* Match container's width */
            margin: 0 auto; /* Center the header */
        }

.container {
            max-width: 600px;
            margin: 0 auto;
            background-color: #ffffff; /* White background for the container */
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
        }

select, input[type="number"] 
        {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 4px;
            border: 1px solid #0077BE; /* Ocean blue border */
            background-color: #f9f9f9; /* Light gray background */
            color: #333; /* Darker text for readability */
        }

button  {
            width: 100%;
            padding: 10px;
            background-color: #0077BE; /* Ocean blue on hover */
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

button:hover 
        {
            background-color: #5D9CEC; /* Light ocean blue button */
        }
#unitConverterHeader 
        {
            color: white; /* Change text color to white */
        }
#result {
            text-align: center;
            margin-top: 20px;
            font-size: 1.2em;
            color: #333; /* Darker text color for the result */
        }

#savedConversions 
        {
            margin-top: 20px;
        }

#savedConversions ul 
        {
            list-style-type: none;
            padding-left: 0;
        }

#savedConversions li 
        {
            background-color: #f1f1f1;
            margin-bottom: 5px;
            padding: 10px;
            border-radius: 4px;
        }
</style>
</head>
<body>

<h1>ENGINEERING UNIT CONVERTER</h1>

<div class="container">
<h2>Conversion</h2>

<label for="conversionType">Choose conversion type:</label>
        <select id="conversionType">
            <option value="length">Length</option>
            <option value="mass">Mass</option>
            <option value="temperature">Temperature</option>
        </select>

<label for="value">Enter value:</label>
        <input type="number" id="value" placeholder="Enter value to convert" />

<label for="fromUnit">From unit:</label>
        <select id="fromUnit"></select>

<label for="toUnit">To unit:</label>
        <select id="toUnit"></select>

<button onclick="performConversion()">Convert</button>

<div id="result"></div>

<div id="savedConversions">
            <h3>Saved Conversions:</h3>
            <ul id="conversionList"></ul>
        </div>
    </div>

<script>
        const lengthUnits = ['km', 'm', 'cm'];
        const massUnits = ['kg', 'g', 'mg'];
        const temperatureUnits = ['Celsius', 'Fahrenheit', 'Kelvin'];

        let savedConversions = [];

        // Populate unit options based on conversion type
        document.getElementById('conversionType').addEventListener('change', updateUnitOptions);
        updateUnitOptions(); // Initial population

        function updateUnitOptions() {
            const type = document.getElementById('conversionType').value;
            let units = [];

            if (type === 'length') {
                units = lengthUnits;
            } else if (type === 'mass') {
                units = massUnits;
            } else if (type === 'temperature') {
                units = temperatureUnits;
            }

            populateSelectOptions('fromUnit', units);
            populateSelectOptions('toUnit', units);
        }

        // Function to populate select options
        function populateSelectOptions(id, units) {
            const select = document.getElementById(id);
            select.innerHTML = ''; // Clear existing options
            units.forEach(unit => {
                const option = document.createElement('option');
                option.value = unit;
                option.textContent = unit;
                select.appendChild(option);
            });
        }

        // Perform the conversion based on user input
        function performConversion() {
            const value = parseFloat(document.getElementById('value').value);
            const fromUnit = document.getElementById('fromUnit').value;
            const toUnit = document.getElementById('toUnit').value;
            const type = document.getElementById('conversionType').value;

            let result;

            if (isNaN(value)) {
                alert("Please enter a valid number.");
                return;
            }

            if (type === 'length') {
                result = convertLength(value, fromUnit, toUnit);
            } else if (type === 'mass') {
                result = convertMass(value, fromUnit, toUnit);
            } else if (type === 'temperature') {
                result = convertTemperature(value, fromUnit, toUnit);
            }

            // Show result
            document.getElementById('result').textContent = `Converted value: ${result}`;

            // Save conversion
            savedConversions.push(`${value} ${fromUnit} to ${toUnit}: ${result}`);
            updateSavedConversions();
        }

        // Conversion functions
        function convertLength(value, from, to) {
            if (from === 'km' && to === 'm') return value * 1000;
            if (from === 'm' && to === 'km') return value / 1000;
            if (from === 'km' && to === 'cm') return value * 100000;
            if (from === 'cm' && to === 'km') return value / 100000;
            if (from === 'm' && to === 'cm') return value * 100;
            if (from === 'cm' && to === 'm') return value / 100;
            return value;
        }

        function convertMass(value, from, to) {
            if (from === 'kg' && to === 'g') return value * 1000;
            if (from === 'g' && to === 'kg') return value / 1000;
            if (from === 'kg' && to === 'mg') return value * 1000000;
            if (from === 'mg' && to === 'kg') return value / 1000000;
            if (from === 'g' && to === 'mg') return value * 1000;
            if (from === 'mg' && to === 'g') return value / 1000;
            return value;
        }

        function convertTemperature(value, from, to) {
            if (from === 'Celsius' && to === 'Fahrenheit') return (value * 9 / 5) + 32;
            if (from === 'Celsius' && to === 'Kelvin') return value + 273.15;
            if (from === 'Fahrenheit' && to === 'Celsius') return (value - 32) * 5 / 9;
            if (from === 'Fahrenheit' && to === 'Kelvin') return (value - 32) * 5 / 9 + 273.15;
            if (from === 'Kelvin' && to === 'Celsius') return value - 273.15;
            if (from === 'Kelvin' && to === 'Fahrenheit') return (value - 273.15) * 9 / 5 + 32;
            return value;
        }

        // Update the list of saved conversions
        function updateSavedConversions() {
            const list = document.getElementById('conversionList');
            list.innerHTML = ''; // Clear the list

            savedConversions.forEach(conversion => {
                const li = document.createElement('li');
                li.textContent = conversion;
                list.appendChild(li);
            });
        }
    </script>

</body>
</html>


 
