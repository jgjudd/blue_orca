<template>
    <div id="company-searchbar-wrapper">
        <label>Company Search: </label>
        <input type="text" v-model="companyName" style="margin-left: 1rem;" />
        <button v-on:click="pullCompanyData">Search</button>
    </div>
    <div v-if="Object.keys(company).length !== 0">
        <h2>{{ company.Name }} - {{ company.Symbol }}</h2>
        <p>{{ company.Address }}</p>
        <div id="company-header">
            <label>Company Description:</label>
            <p>{{ company.Description }}</p>
        </div>
        <h4>Company Info</h4>
        <div id="company-info-wrapper">
            <div>
                <p><span style="font-weight:bold;">Asset Type:</span> {{ company.AssetType }}</p>
                <p><span style="font-weight:bold;">CIK:</span> {{ company.CIK }}</p>
                <p><span style="font-weight:bold;">Exchange:</span> {{ company.Exchange }}</p>
                <p><span style="font-weight:bold;">Currency:</span> {{ company.Currency }}</p>
                <p><span style="font-weight:bold;">Country:</span> {{ company.Country }}</p>
                <p><span style="font-weight:bold;">Sector:</span> {{ company.Sector }}</p>
                <p><span style="font-weight:bold;">Industry:</span> {{ company.Industry }}</p>
                <p><span style="font-weight:bold;">Fiscal Year End:</span> {{ company.FiscalYearEnd }}</p>
                <p><span style="font-weight:bold;">Latest Quarter:</span> {{ company.LatestQuarter }}</p>
                <p><span style="font-weight:bold;">Market Capitalization:</span> {{ company.MarketCapitalization }}</p>
                <p><span style="font-weight:bold;">EBITDA:</span> {{ company.EBITDA }}</p>
            </div>
            <div>
                <p><span style="font-weight:bold;">PE Ration:</span> {{ company.PERatio }}</p>
                <p><span style="font-weight:bold;">PEG Ratio:</span> {{ company.PEGRatio }}</p>
                <p><span style="font-weight:bold;">Book Value:</span> {{ company.BookValue }}</p>
                <p><span style="font-weight:bold;">Dividend Per Share:</span> {{ company.DividendPerShare }}</p>
                <p><span style="font-weight:bold;">Dividend Yield:</span> {{ company.DividendYield }}</p>
                <p><span style="font-weight:bold;">EPS:</span> {{ company.EPS }}</p>
                <p><span style="font-weight:bold;">Revenue Per Share TTM:</span> {{ company.RevenuePerShareTTM }}</p>
                <p><span style="font-weight:bold;">Profit Margin:</span> {{ company.ProfitMargin }}</p>
                <p><span style="font-weight:bold;">Operating Margin TTM:</span> {{ company.OperatingMarginTTM }}</p>
                <p><span style="font-weight:bold;">Return On Assets TTM:</span> {{ company.ReturnOnAssetsTTM }}</p>
            </div>
            <div>
                <p><span style="font-weight:bold;">Return On Equity TTM:</span> {{ company.ReturnOnEquityTTM }}</p>
                <p><span style="font-weight:bold;">Revenue TTM:</span> {{ company.RevenueTTM }}</p>
                <p><span style="font-weight:bold;">Gross Profit TTM:</span> {{ company.GrossProfitTTM }}</p>
                <p><span style="font-weight:bold;">Return On Equity TTM:</span> {{ company.ReturnOnEquityTTM }}</p>
                <p><span style="font-weight:bold;">Diluted EPS TTM:</span> {{ company.DilutedEPSTTM }}</p>
                <p><span style="font-weight:bold;">Quarterly Earnings Growth YOY:</span> {{ company.QuarterlyEarningsGrowthYOY }}</p>
                <p><span style="font-weight:bold;">Qaurterly Revenue Growth YOY:</span> {{ company.QuarterlyRevenueGrowthYOY }}</p>
                <p><span style="font-weight:bold;">Target Price:</span> {{ company.AnalystTargetPrice }}</p>
                <p><span style="font-weight:bold;">Trailing PE:</span> {{ company.TrailingPE }}</p>
                <p><span style="font-weight:bold;">Forward PE:</span> {{ company.ForwardPE }}</p>
            </div>
            <div>
                <p><span style="font-weight:bold;">Price To Sales Ratio TTM:</span> {{ company.PriceToSalesRatioTTM }}</p>
                <p><span style="font-weight:bold;">Price To Book Ratio:</span> {{ company.PriceToBookRatio }}</p>
                <p><span style="font-weight:bold;">EV To Revenue:</span> {{ company.EVToRevenue }}</p>
                <p><span style="font-weight:bold;">EV To EBITDA:</span> {{ company.EVToEBITDA }}</p>
                <p><span style="font-weight:bold;">Beta:</span> {{ company.Beta }}</p>
                <p><span style="font-weight:bold;">52 Week High:</span> {{ company["52WeekHigh"] }}</p>
                <p><span style="font-weight:bold;">52 Week Low:</span> {{ company["52WeekLow"] }}</p>
                <p><span style="font-weight:bold;">50 Day Moving Average:</span> {{ company["50DayMovingAverage"] }}</p>
                <p><span style="font-weight:bold;">200 Day Moving Average:</span> {{ company["200DayMovingAverage"] }}</p>
                <p><span style="font-weight:bold;">Shares Outstanding:</span> {{ company.SharesOutstanding }}</p>
                <p><span style="font-weight:bold;">Dividend Date:</span> {{ company.DividendDate }}</p>
                <p><span style="font-weight:bold;">Ex Dividend Date:</span> {{ company.ExDividendDate }}</p>
            </div>
        </div>
        <div>
            <h4>Balance Sheets (Per Year)</h4>
            <table></table>
        </div>
        <div>
            <h4>Cash Flow</h4>
            <table></table>
        </div>
        <div>
            <h4>Income Statements (Annual)</h4>
            <table></table>
        </div>
        <div>
            <h4>Income Statements (Quarterly)</h4>
            <table></table>
        </div>
    </div>
</template>

<script>
export default {
  name: 'CompanyData',
  data () {
    return {
      companyName: '',
      company: {},
      annualReports: [],
      quarterlyReports: []
    }
  },
  methods: {
    async pullCompanyData () {
      const term = this.companyName.toUpperCase()
      alert('Company Search Submitted -----> Company: ' + term)
      const companyResults = await fetch(`https://www.alphavantage.co/query?function=OVERVIEW&symbol=${term}&apikey=16RM7YB3WU85H52Z`)
        .then(res => res.json())
      this.company = companyResults
      const incomeResults = await fetch(`https://www.alphavantage.co/query?function=INCOME_STATEMENT&symbol=${term}&apikey=16RM7YB3WU85H52Z`)
        .then(res => res.json())
      this.annualReports = incomeResults.annualReports
      console.log(this.annualReports)
      this.quarterlyReports = incomeResults.quarterlyReports
      console.log(this.quarterlyReports)
    }
  }
}

</script>

<style>
    #company-info-wrapper {
        display: flex;
        justify-content: space-between;
        text-align: left;
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
