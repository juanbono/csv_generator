This library provides an easy way to generate CSV files.
It allows you to define the colums and their respective types.

## Example

    defmodule MyCSV do
      use CsvGenerator

      column :name, :string
      column :joined, :date, format: "%d-%m-%Y"
      column :points, :integer, label: "points earned"
    end

You would then render the CSV bij calling the `render/1` method with
the list of lines to render.

## Example

    iex> MyCSV.render([ 
       %{ name: "Chris McCord", joined: ~D[2020-01-01], points: 110},
       %{ name: "Jose Valim", joined: ~D[2020-03-29], points: 10} ])
    "\"name\",\"joined\",\"points earned\"\n\"Chris McCord\",01-01-2020,110\n\"Jose Valim\",29-03-2020,10"

By default the CSV columns will be seperated by a `","`, the lines by a `"\n"`.
This can be changed by using `delimiter` and `line_ending`.

## Example

    defmodule MyCSV do
      use CsvGenerator

      delimiter ";"
      line_ending "\r\n"

      column :name, :string
      column :birthday, :date, format: "%d-%m-%Y"
      column :points, :integer
    end

    iex> MyCSV.render([ 
       %{ name: "Jose Valim", joined: ~D[2020-03-29], points: 10} ])
    "\"name\";\"joined\";\"points earned\"\n\"Jose Valim\";29-03-2020;10"

