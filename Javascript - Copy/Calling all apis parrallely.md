we can use promise .all for fetching all apis parallely

```
const fetchLocationData = async () => {

        const promises = [];

  

        promises.push(fetchDropdownData('communicationAddress', data, lazyGetNewCountriesQuery, setCountryDropdown, 'region'));

        promises.push(fetchDropdownData('communicationAddress', data, lazyGetNewStatesQuery, setStateDropdown, 'country'));

        promises.push(fetchDropdownData('communicationAddress', data, lazyGetNewCitiesQuery, setCityDropdown, 'state'));

  

        promises.push(fetchDropdownData('billingAddress', data, lazyGetNewCountriesQuery, setBillCountryDropdown, 'region'));

        promises.push(fetchDropdownData('billingAddress', data, lazyGetNewStatesQuery, setBillStateDropdown, 'country'));

        promises.push(fetchDropdownData('billingAddress', data, lazyGetNewCitiesQuery, setBillCityDropdown, 'state'));

  

        // Wait for all promises to resolve

        await Promise.all(promises);

    };
```