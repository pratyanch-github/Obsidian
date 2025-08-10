[[Redux types, slices and endpoints]]  
[[]]
1. i have completed the facility page
          -  table completed 
          - [ ]  default mrt options not working (have to discuss with Ayyappa) 
          - [ ]   [**System keys**]([Properties - MUI System](https://mui.com/system/properties/)). The column lists the key(s) by which you can use this property with the `sx` prop (or as a system function). - three ways to give stypes to mui components, and use comma for multiple styles. 📝
    
    ```jsx
    <Button sx={{ mb: 3 }}>
    // or
    <Box mb={3}>
    // or
    <Box marginBottom={3}>
    ```
1.   Linking add organization with Addorg page  
          - create react route in routes with query params- ✅
          - Linked routes with row action of facility table- ✅
2. creating 3 api endpints 
          - addOrg-> put , for adding new Ogr, from org button, legal-str and optionals
          - EditOrg-> patch,  from org id 
          - getOrg-> get,  from org id
  3. in addorg component , reading value of undefined error is comming from enabeling dropdown and not giving options , because dropdown reads options, 

