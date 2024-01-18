# OOPs
Object Oriented Programming

App.js
return (
    <div className="App">
  
      <header className="App-header">
        <h1>What's Priced In? Hahaha</h1>
      </header>
  
      <div className="container">
        <div className="currency-selection">
          <label htmlFor="live-currencies" className="currency-selection-label">Live Currencies</label>
            <CurrencySelection 
              options={currencyOptions}
              selectedCurrency={selectedCurrency}
              onCurrencyChange={setSelectedCurrency}
            />
        </div>
  
      <div className="historic-selection">
        <label className="historic-selection-label">Historic Currency Selection</label>
          <div className="selectors-container">
            {selectors.map((selector, index) => (
              <CurrencyDateSelector
                key={index}
                selectedCurrency={selector.selectedCurrency}
                onCurrencyChange={(currency) => handleCurrencyChange(index, currency)}
                selectedDate={selector.selectedDate}
                onDateChange={(date) => handleDateChange(index, date)}
                currencyOptions={currencyOptions}
              />
            ))}
          </div>
      </div>
  
      <div className="chart-container">
        <h2 className="chart-title">This is Priced!</h2>
        <CurrencyChart chartData={combineChartData([chartData, ...chartDatasets])} />
      </div>  
  
        {selectedCurrency.map((currency, index) => (
          <CurrencyTable key={index} selectedCurrency={currency.value} />
        ))}
  
        {tableDataSets.map((tableData, index) => (
          <CurrencyTable key={index} tableData={tableData} />
        ))}
      </div>
  
    </div>
  );  
}

export default App;

curr-date-sel
    return (
        <div className="currency-date-selector">
            <Select
                className="currency-select"
                value={currencyOptions.find(option => option.value === selectedCurrency)}
                onChange={option => onCurrencyChange(option.value)}
                options={currencyOptions}
                isClearable
            />
            <DatePicker
                selected={selectedDate|| oneWeekAgo}
                onChange={onDateChange}
                wrapperClassName="date-picker-wrapper"
            />
        </div>
    );

curr-sel
const CurrencySelection = ({options, selectedCurrency, onCurrencyChange }) => {

  return (
    <div className='currency-select-container'>
      <Select
        isMulti
        options={options}
        value={selectedCurrency}
        onChange={onCurrencyChange}
        styles={customStyles}
        className="currency-select"
        classNamePrefix="select"
        placeholder="Select currencies..."
      />
    </div>
  );
};


curr-table

  return (
      <div className='currency-table-container'>
        <div>
          <h2 className='currency-table-title'>Table for {selectedCurrency}</h2>
            {isLoading && <p>Loading...</p>}
            {error && <p>Error loading data</p>}
            {!isLoading && !error && (
            <table className='currency-table'>
              <thead>
                <tr>
                  {tableData.columns.map((column, index) => (
                    <th key={index}>{column}</th>
                  ))}
                </tr>
              </thead>
            <tbody>
            {tableData.data.map((row, rowIndex) => (
            <tr key={rowIndex}>
              {row.map((cell, cellIndex) => (
              <td key={cellIndex}>{cell}</td>
              ))}
            </tr>
            ))}
            </tbody>
            </table>
          )}
        </div>
      </div>
  );

