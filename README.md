# YahooApi

using System;
using System.Threading.Tasks;
using YahooFinanceApi;

namespace ConsoleApp2
{
    class Program
    {
        static async Task MainAsync(string[] args)
        {
            string MarsResponse = await QueryRover();            

            Console.WriteLine(MarsResponse);
        }    
        static async Task<string> QueryRover()
        { 
            // You could query multiple symbols with multiple fields through the following steps:
            var securities = await Yahoo.Symbols("AAPL", "GOOG").Fields(Field.Symbol, Field.RegularMarketPrice, Field.FiftyTwoWeekHigh).QueryAsync();
            var aapl = securities["AAPL"];
            var price = aapl[Field.RegularMarketPrice]; // or, you could use aapl.RegularMarketPrice directly for typed-value
            return Convert.ToInt64(price);
        }
    }
}
