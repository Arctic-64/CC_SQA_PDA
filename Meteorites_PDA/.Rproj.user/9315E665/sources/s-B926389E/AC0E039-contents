library(janitor)
library(tidyverse)
library(assertr)
library(testthat)
library(here)
#3.1 process data from external file
meteorites = read.csv(here("raw_data/meteorite_landings.csv"))
meteorites = janitor::clean_names(meteorites)

#3.3 clean data
meteorites = mutate(meteorites, geo_location = str_sub(geo_location, 2, -2))
meteorites = separate(meteorites, geo_location, into = c("lattitude", "longditude"), sep = ", ")

meteorites = mutate(meteorites, lattitude = replace_na(lattitude, "0"))
meteorites = mutate(meteorites, longditude = replace_na(longditude, "0"))

meteorites = filter(meteorites, mass_g > 1000)

meteorites = arrange(meteorites, year)

meteorites = mutate(meteorites, lattitude = as.numeric(lattitude))
meteorites = mutate(meteorites, longditude = as.numeric(longditude))

verify(meteorites, lattitude > -90.0 & lattitude < 90.0 & longditude > -180.0 & longditude < 180.0)
verify(meteorites, has_all_names("id", "name", "mass_g", "fall", "year", "lattitude", "longditude"))
print("TESTS PASSED")

write.csv(meteorites, here("clean_data/meteorite_landings_CLEAN.csv"))

