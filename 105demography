#!/usr/bin/env python3
##
## EPITECH PROJECT, 2023
## Project Math
## File description:
## 105demography
##

import math
import csv
import sys


class DemographyAnalyzer:
    def __init__(self, data_file='105demography_data.csv'):
        self.data = self.load_data(data_file)
        self.country_codes = [line[1] for line in self.data]
        self.country_names = [line[0] for line in self.data]

    def load_data(self, file_name):
        with open(file_name, 'r') as data_file:
            reader = csv.reader(data_file, delimiter=';')
            return list(reader)[1:]

    def get_sums(self, tab, is_type_2: bool):
        sums = [0, 0, 0, 0]
        years = list(range(1960, 2018))

        for i in range(len(tab)):
            if is_type_2:
                sums[0] += years[i]
                sums[1] += tab[i]
                sums[2] += pow(tab[i], 2)
                sums[3] += tab[i] * years[i]
            else:
                sums[0] += tab[i]
                sums[1] += years[i]
                sums[2] += pow(years[i], 2)
                sums[3] += tab[i] * years[i]
        return sums, years

    def mean(self, values):
        if not values:
            return 0.0
        return sum(values) / len(values)

    def covariance(self, x, mean_x, y, mean_y):
        covar = 0.0
        for i in range(len(x)):
            covar += (x[i] - mean_x) * (y[i] - mean_y)
        return covar

    def variance(self, values, mean):
        return sum([(x - mean) ** 2 for x in values])

    def fcorrelation(self, X, Y):
        correlation = self.covariance(Y, self.mean(Y), X, self.mean(X)) / (
                math.sqrt(self.variance(Y, self.mean(Y))) * math.sqrt(self.variance(X, self.mean(X))))
        return correlation

    def linear_function(self, sums, years):
        a = (sums[0] * sums[2] - sums[1] * sums[3]) / (len(years) * sums[2] - sums[1] ** 2)
        b = ((len(years) * sums[3]) - (sums[0] * sums[1])) / ((len(years) * sums[2]) - math.pow(sums[1], 2))
        if a >= 0:
            print(f"    X = {b * 1000000:.2f} Y + {a:.2f}")
        else:
            print(f"    Y = {b / 1000000:.2f} X - {a / 1000000 * -1:.2f}")
        return a, b

    def Fit1(self, populations_total, years):
        print("Fit 1")
        sums, _ = self.get_sums(populations_total, False)
        a, b = self.linear_function(sums, years)
        res = sum((years[i] * b + a - populations_total[i]) ** 2 for i in range(len(populations_total))) / len(
            populations_total)
        print(f"    Root-mean-square deviation: {math.sqrt(res) / 1e6:.2f}")
        print(f"    Population in 2050: {(2050 * b + a) / 1e6:.2f}")

    def Fit2(self, populations_total, years):
        print("Fit 2")
        sums, _ = self.get_sums(populations_total, True)
        a, b = self.linear_function(sums, years)
        res = sum(((years[i] - a) / b - populations_total[i]) ** 2 for i in range(len(populations_total))) / len(
            populations_total)
        print(f"    Root-mean-square deviation: {math.sqrt(res) / 1e6:.2f}")
        print(f"    Population in 2050: {((2050 - a) / b) / 1e6:.2f}")

    def compare_country(self, inputed_codes):
        index = []
        for code in inputed_codes:
            if code in self.country_codes:
                index.append(self.country_codes.index(code))
            else:
                print(f"{code} is not a valid country code")
        if not index:
            print("Please enter at least one valid country code")
            exit(84)
        return index

    def select_inputed_countries(self, index):
        countries = []
        for i in index:
            countries.append(self.data[i][2:])
        return countries

    def countries_total(self, countries):
        total_countries = [sum(int(value) for value in year_data) for year_data in zip(*countries)]
        return total_countries

    def do_math(self, inputed_codes):
        index = self.compare_country(inputed_codes)
        countries = self.select_inputed_countries(index)
        total_countries = self.countries_total(countries)

        # Write the countries
        temp_country_names = ""
        for line in self.data:
            if line[1] in inputed_codes:
                temp_country_names += line[0]
                temp_country_names += ", "

        temp_country_names = temp_country_names[:-2]
        print(f"Country: {temp_country_names}")

        self.Fit1(total_countries, list(range(1960, 2018)))
        self.Fit2(total_countries, list(range(1960, 2018)))
        print(f"Correlation: {self.fcorrelation(total_countries, list(range(1960, 2018))):.4f}")
        return 0


if __name__ == "__main__":
    # Handle -h option
    if len(sys.argv) > 1 and sys.argv[1] == '-h':
        print("USAGE\n    ./105demography [code]+\n\nDESCRIPTION\n    code    country code")
        exit(1)

    # Remove first argument (program name)
    argv = sys.argv[1:]

    analyzer = DemographyAnalyzer()
    analyzer.do_math(argv)
