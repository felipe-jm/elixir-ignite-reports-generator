<h1 align="center">
    <img width="120" alt="Ignite" src="https://res.cloudinary.com/dqcqifjms/image/upload/v1615216700/felipejung/ignite.png" />
    <br>
    Ignite - Elixir - Reports Generator
</h1>

<h4 align="center">
  A simple application that reads a csv and returns some information about it
</h4>

## :information_source: How To Use

```bash
# In your terminal, open iex:
iex -S mix

# Sum of how many money each user spent:
iex(1)> ReportsGenerator.build("report_complete.csv")
%{
  "foods" => %{
    "açaí" => 37742,
    "churrasco" => 37650,
    "esfirra" => 37462,
    "hambúrguer" => 37577,
    "pastel" => 37392,
    "pizza" => 37365,
    "prato_feito" => 37519,
    "sushi" => 37293
  },
  "users" => %{
    "1" => 278849,
    "10" => 268317,
    "11" => 268877,
    "12" => 276306,
    "13" => 282953,
    "14" => 277084,
    "15" => 280105,
    "16" => 271831,
    "17" => 272883,
    "18" => 271421,
    "19" => 277720,
    "2" => 271031,
    "20" => 273446,
    "21" => 275026,
    "22" => 278025,
    "23" => 276523,
    "24" => 274481,
    "25" => 274512,
    "26" => 274199,
    "27" => 278001,
    "28" => 274256,
    "29" => 273030,
    "3" => 272250,
    "30" => 275978,
    "4" => 277054,
    "5" => 270926,
    "6" => 272053,
    "7" => 273112,
    "8" => 275161,
    "9" => 274003
  }
}

# Get the user who spent the most money:
iex(2)> ReportsGenerator.build("report_complete.csv") |> ReportsGenerator.fetch_higher_cost("users")
{:ok, {"13", 282953}}

# Get the most consumed food:
iex(3)> ReportsGenerator.build("report_complete.csv") |> ReportsGenerator.fetch_higher_cost("foods")
{:ok, {"açaí", 37742}}
```

## :zap: :clock10: Performance

Using the following command, we are reading a CSV file with 300 thousand lines and measuring how many microseconds it took:

```elixir
iex(1)> :timer.tc(fn -> ReportsGenerator.build("report_complete.csv") end)
{674379,
 %{
   "foods" => %{
     "açaí" => 37742,
     "churrasco" => 37650,
     "esfirra" => 37462,
     "hambúrguer" => 37577,
     "pastel" => 37392,
     "pizza" => 37365,
     "prato_feito" => 37519,
     "sushi" => 37293
   },
   "users" => %{
     "1" => 278849,
     "10" => 268317,
     "11" => 268877,
     "12" => 276306,
     "13" => 282953,
     "14" => 277084,
     "15" => 280105,
     "16" => 271831,
     "17" => 272883,
     "18" => 271421,
     "19" => 277720,
     "2" => 271031,
     "20" => 273446,
     "21" => 275026,
     "22" => 278025,
     "23" => 276523,
     "24" => 274481,
     "25" => 274512,
     "26" => 274199,
     "27" => 278001,
     "28" => 274256,
     "29" => 273030,
     "3" => 272250,
     "30" => 275978,
     "4" => 277054,
     "5" => 270926,
     "6" => 272053,
     "7" => 273112,
     "8" => 275161,
     "9" => 274003
   }
 }}
```

It took 674379 microseconds, equivalent to 674,379 milliseconds

Now readind three files (_this files together form the 300 thousand lines csv_) in parallel using a task with three processes:

```elixir
iex(2)> :timer.tc(fn -> ReportsGenerator.build_from_many(["report_1.csv", "report_2.csv", "report_3.csv"]) end)
{207980,
 %{
   "foods" => %{
     "açaí" => 37742,
     "churrasco" => 37650,
     "esfirra" => 37462,
     "hambúrguer" => 37577,
     "pastel" => 37392,
     "pizza" => 37365,
     "prato_feito" => 37519,
     "sushi" => 37293
   },
   "users" => %{
     "1" => 278849,
     "10" => 268317,
     "11" => 268877,
     "12" => 276306,
     "13" => 282953,
     "14" => 277084,
     "15" => 280105,
     "16" => 271831,
     "17" => 272883,
     "18" => 271421,
     "19" => 277720,
     "2" => 271031,
     "20" => 273446,
     "21" => 275026,
     "22" => 278025,
     "23" => 276523,
     "24" => 274481,
     "25" => 274512,
     "26" => 274199,
     "27" => 278001,
     "28" => 274256,
     "29" => 273030,
     "3" => 272250,
     "30" => 275978,
     "4" => 277054,
     "5" => 270926,
     "6" => 272053,
     "7" => 273112,
     "8" => 275161,
     "9" => 274003
   }
 }}
```

It took 207980 microseconds, equivalent to 207,98 milliseconds! A difference of 466,399 milliseconds!

## :heavy_check_mark: Running the tests

```bash
mix test
.....

Finished in 0.02 seconds
5 tests, 0 failures

Randomized with seed 188490
```

## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/felipe-jm/elixir-ignite-reports-generator/blob/master/LICENSE) for more information.

---

Made with much :heart: and :muscle: by Felipe Jung :blush: <a href="https://www.linkedin.com/in/felipe-jung/">Talk to me!</a>
