1. typescript automatically infers types -  if assigned value![[Pasted image 20240221110141.png]]

2.    
      import React, { useState } from 'react';
import { Select, MenuItem, FormControl, InputLabel } from '@mui/material';

function MySelect() {
    const [selectedValue, setSelectedValue] = useState('');

    const handleChange = (event) => {
        setSelectedValue(event.target.value);
    };

    return (
        <FormControl>
            <InputLabel id="demo-simple-select-label">Select an option</InputLabel>
            <Select
                labelId="demo-simple-select-label"
                id="demo-simple-select"
                value={selectedValue} // this value is assigned to this select after handelchange gives a value to selectedValue, this is just for display, this is not the value present in event.target.value
                onChange={handleChange}
            >
                <MenuItem value={'option1'}>Option 1</MenuItem>
                <MenuItem value={'option2'}>Option 2</MenuItem>
                <MenuItem value={'option3'}>Option 3</MenuItem>
            </Select>
        </FormControl>
    );
}

--// selectedvalue  value is assigned to this select after handelchange gives a value to selectedValue, this is just for display, this is not the value present in event.target.value

