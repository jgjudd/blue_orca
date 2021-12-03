<template>
    <div id="company-searchbar-wrapper">
        <label>Company Search: </label>
        <input type="text" v-model="companyName" style="margin-left: 1rem;" />
        <button v-on:click="pullCompanyData">Search</button>
    </div>
    <div v-if="Object.keys(company).length !== 0">
        <h2>{{ company.Name }} - {{ company.Symbol }}</h2>
        <div id="company-header">
            <label>Company Description:</label>
            <p>{{ company.Description }}</p>
            <label>Asset Type:</label>
            <p>{{ company.AssetType }}</p>
        </div>
        <div id="company-info-wrapper">
            <p>CIK: {{ company.CIK }}</p>
            <p>Exchange: {{ company.Exchange }}</p>
            <p>Currency: {{ company.Currency }}</p>
            <p>Country: {{ company.Country }}</p>
            <p>Sector: {{ company.Sector }}</p>
            <p>Industry: {{ company.Industry }}</p>
            <p>Address: {{ company.Address }}</p>
            <p>Fiscal Year End: {{ company.FiscalYearEnd }}</p>
            <p>Latest Quarter: {{ company.LatestQuarter }}</p>
            <p>Market Capitalization: {{ company.MarketCapitalization }}</p>
            <p>EBITDA: {{ company.EBITDA }}</p>
            <p>PE Ration: {{ company.PERatio }}</p>
            <p>PEG Ratio: {{ company.PEGRatio }}</p>
            <p>Book Value: {{ company.BookValue }}</p>
            <p>Dividend Per Share: {{ company.DividendPerShare }}</p>
            <p>Dividend Yield: {{ company.DividendYield }}</p>
            <p>EPS: {{ company.EPS }}</p>
            <p>Revenue Per Share TTM: {{ company.RevenuePerShareTTM }}</p>
            <p>Profit Margin: {{ company.ProfitMargin }}</p>
            <p>Operating Margin TTM: {{ company.OperatingMarginTTM }}</p>
            <p>Return On Assets TTM: {{ company.ReturnOnAssetsTTM }}</p>
            <p>Return On Equity TTM: {{ company.ReturnOnEquityTTM }}</p>
            <p>Revenue TTM: {{ company.RevenueTTM }}</p>
            <p>Gross Profit TTM: {{ company.GrossProfitTTM }}</p>
            <p>Return On Equity TTM: {{ company.ReturnOnEquityTTM }}</p>
            <p>Diluted EPS TTM: {{ company.DilutedEPSTTM }}</p>
            <p> Quarterly Earnings Growth YOY: {{ company.QuarterlyEarningsGrowthYOY }}</p>
            <p>Qaurterly Revenue Growth YOY: {{ company.QuarterlyRevenueGrowthYOY }}</p>
            <p>Analyst Target Price: {{ company.AnalystTargetPrice }}</p>
            <p>Trailing PE: {{ company.TrailingPE }}</p>
            <p>Forward PE: {{ company.ForwardPE }}</p>
            <p>Price To Sales Ratio TTM: {{ company.PriceToSalesRatioTTM }}</p>
            <p>Price To Book Ratio: {{ company.PriceToBookRatio }}</p>
            <p>EV To Revenue: {{ company.EVToRevenue }}</p>
            <p>EV To EBITDA: {{ company.EVToEBITDA }}</p>
            <p>Beta: {{ company.Beta }}</p>
            <p>52 Week High: {{ company["52WeekHigh"] }}</p>
            <p>52 Week Low: {{ company["52WeekLow"] }}</p>
            <p>50 Day Moving Average: {{ company["50DayMovingAverage"] }}</p>
            <p>200 Day Moving Average: {{ company["200DayMovingAverage"] }}</p>
            <p>Shares Outstanding: {{ company.SharesOutstanding }}</p>
            <p>Dividend Date: {{ company.DividendDate }}</p>
            <p>Ex Dividend Date: {{ company.ExDividendDate }}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'CompanyData',
  data () {
    return {
      companyName: '',
      company: {}
    }
  },
  methods: {
    async pullCompanyData () {
      const term = this.companyName.toUpperCase()
      alert('Company Search Submitted -----> Company: ' + term)
      const results = await fetch(`https://www.alphavantage.co/query?function=OVERVIEW&symbol=${term}&apikey=16RM7YB3WU85H52Z`)
        .then(res => res.json())
      this.company = results
      console.log(this.company.Name)
    }
  }
}

</script>

<style>
    #company-info-wrapper {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }
    #company-header {
        text-align: left;
    }
    label {
        font-weight: bold;
    }
    #company-searchbar-wrapper {
        display: flex;
        align-items: center;
    }
</style>
