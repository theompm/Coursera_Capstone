# The Battle of Neighborhoods (Week 1)

## Introduction

### Description of the problem and a discussion of the background
Munich is the capital of bavaria. It is a global centre of:

- art
- science
- technology
- finance
- publishing
- culture
- innovation
- education
- business
- tourism

Because of these attributes a friend of mine decided moving to munich. He asked me helping him choosing the right district to live in.


### Description of the data and how it will be used to solve the problem 

The first dataset is from [https://www.dasoertliche.de](https://www.dasoertliche.de/Themen/Postleitzahlen/M%C3%BCnchen.html).

Including:

- Postal Code
- Town Name
- District
- Borough
- State

With *Nominatim* from the library *geopy.geocoders* we will get the centered geographical coordinates of districts.

Get the venues from *Foursquare API* searching by coordinates.

With this data we will create a map and information chart of clusters to solve the problem.
