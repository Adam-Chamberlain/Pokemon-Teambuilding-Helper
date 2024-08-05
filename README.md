# Pokemon Teambuilding Helper

## Introduction

Competitive Pokemon battling has been a hobby of mine for many years, and recently, I have especially found an interest in using my growing Microsoft Excel / Google Sheets knowledge to make resources for the community. There are many different ways to play the game, but in this instance, each player creates a team of a set number of Pokemon (usually 8, but sometimes up to 12), and they must pick six of them to counter-team opposing teams. While it may sound simple, competitive Pokemon actually has a lot of depth in it; each Pokemon can be used dozens of different ways, and their stats can be modified in order to more effectively counter opponents. This is a lot to handle, especially for newer players, and many people, myself included, enjoy visuals that lay out all of the important info in a simplified and aesthetically pleasing way.

In early 2023, I created this resource to help people in their teambuilding process. It started as a small project, but as time went on, more people began using it, and I added many different features to account for different ways people play the game. Now, it covers over 10 different formats, and an estimated 600+ people use it on a weekly basis, and many have pointed to it as a reason they have been able to significantly improve their competitive performance.

This resource was made in Google Sheets, and it uses hundreds of in-depth functions to be fully automated. I have spent many hours testing and modifying this resource to make it as effective and easy to use as possible. Here is a link to an example if you would like to take a look: https://docs.google.com/spreadsheets/d/15LqEfyx0zXVuaEk-h-9Z1kmqXROyIVTEOkIdZ5cMfIA/edit?usp=sharing

## Brief Overview

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/3e89e38a-7be5-470e-8137-6008e33fdc70)

The spreadsheet consists of multiple tabs in order to stay organized. This is the "Home" tab, which shows a quick overview graphic of a selected matchup. The team selected is called "Example", and the selected format is "National Dex", which includes every Pokemon that exists, regardless of if it is available in the most recent video games. Many formats exist, typically based on different entries in the video game franchise.

Throughout the spreadsheet, blue represents the user's team, and red represents the opposing team. In the middle, the "Speed Tiers" show what each Pokemon's Speed stat is. This is important for users to know because faster Pokemon always attack before slower ones.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/6cabcc37-df5e-4fcd-875c-537f685f2107)

This is the "Teams" tab, which is the only place data is manually inputted. This is where users put their teams and change the team name and format. It can support up to 15 different teams, which can be swapped between at any time.

- "Cpt" stands for Captain, which are Pokemon that can use specific mechanics that exist in some games, such as the ability to change its type or gain a single-use move that does much more damage. In these cases, their name and image on the Home tab turn yellow using conditional formatting to easily differentiate them.
- In many scenarios, teams must be created on a budget, and Pokemon are priced based on how strong they are. The "Cost" column lets users easily calculate how many points they have remaining based on a specific budget. (In the example, 90)

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/df6e9a19-c9dc-46a0-ab2f-d41284e938ea)

Here is the "Matchup" page, which has much more detailed information about a given matchup. The team is selected by the dropdown in the top left corner, which shows all 15 available teams via data validation. This tab includes Pokemon's types, stats, and abilities, which are all important traits to be aware of. It can also be sorted in many different ways, including by a specific stat (such as Speed), alphabetically, and the same order from the Teams page.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/144f75dc-3dd9-4614-b307-87f70b367391)

Also on the Matchup page, this chart shows how effective each type is against a given Pokemon. For example, Dugtrio at the top takes 0x damage from Electric attacks, but it takes 2x damage from Ice attacks. This chart lets users easily see if they have a major weakness within their team.

- The last few rows are empty because the resource supports teams of up to 12 Pokemon, and this example only has 8.
- "Count" shows how many Pokemon of a specific type are on the team. It's generally better to have a variety of types in order to not be very weak to specific types, making it a good piece of info for users to be aware of.
- "Weak" is a mathematical formula that shows approximately how weak the team is in total to a given type. For example, Rock is the biggest weakness on the top team because it has three Pokemon weak to it (two that take 2x damage and one that takes 4x damage) and only one that takes less-than-normal damage (0.5x) from it. The full breakdown for how it's calculated is below:

```
Positive: More Resistant than Weak
0: Neutral
Negative: More Weak than Resistant

No resistances: -2
Only one resistance: -1

+2 - 0.25x, 0.125x, 0x
+1 - 0.5x
-1 - 2x
-2 - 4x, 8x
```

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/6d2e96da-af14-42ab-92cf-e62427434305)

The "Moves" tab shows key moves that Pokemon on the team get. These moves are important for users to take note of when creating a team and preparing against an opposing team. This tab has two modes: "Singles", which is 1 versus 1, and "Doubles", which is 2 versus 2. The two modes play very differently, so different moves are relevant within each.

## How it Works

In order to make this spreadsheet as user-friendly as possible, I put a lot of work into optimizing the backend code, which consists of three sections:

- **Pokedex** - List of Pokemon names along with their icons and stats
- **Format Tabs**: List of Pokemon's specific stats and moves within a given format
- **Backend**: Where all of the code comes together

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/ea9856e6-f8ea-442c-bc48-e391cec08a77)

The "Pokedex" tab lists every single Pokemon as well as their icons, which are used throughout the resource. This allows for two things: Data Validation to ensure that only Pokemon names are inputted in certain fields, and VLOOKUP formulas to search for sprites or other information. For example, this formula is very frequently used:
```
=IFERROR(ARRAYFORMULA(VLOOKUP(C4:C15,Pokedex!$C$2:$D,2,false)))
```
Range C4:C15 has a list of Pokemon, and the range C2:D on the Pokedex tab has names in the first column and icons in the second. It pulls icons based on the given name.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/214b27dd-a48f-40ba-b5fa-d09c35bc7468)

To grab each Pokemon's stats, typings, and abilities, it gets a little more complicated. Throughout different games and formats, Pokemon have had their stats changed, and some Pokemon simply do not exist in older games. So for this, there is a hidden tab for each format that only lists the available Pokemon as well as their stats within that format. Above is an example, with each format looking slightly different.

I use INDIRECT formulas to pull this data based on the format selected. For example:
```
=IFERROR(ARRAYFORMULA(VLOOKUP(G62:G73,INDIRECT($C64&"!$B$2:$N"),{9,10,8,2,3,4,5,6,7,11,12,13},FALSE)),"")
```
This formula is what pulls all of the data to the right of the Pokemons' names in the below image. In this case, "C64" is the selected format, which is "National Dex". Using INDIRECT, it searches cells B2:N on the "National Dex" tab. If the format were to be changed, it would search a different tab instead.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/a59edd31-0ece-420f-87ae-8ed9f1981268)

The "Backend" tab is where it all comes together. It first pulls all 15 teams from the "Teams" page. In this case, the "Example" team is Team 6. It then uses VLOOKUP to find all of each Pokemon's stats in the correct format. The exact same formula is used for the opponent's teamm, which is located to the right of this image. The numbers in columns A and D allow me to use FILTER commands in order to create the "Home" tab. For example:
```
=FILTER(Backend!$L$2:$L,Backend!$B$2:$B=C2,Backend!$D$2:$D=1)
```
This looks at column L, where the Pokemon's names are located, then checks which rows equal the selected team shown on cell C2 (Example), and then it checks which row within that equals "1" in column D. That ends up being Venusaur.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/4bda5617-ba0c-451f-bb5d-20d22af9199f)

Also on the Backend tab, I sort the selected team by their Speed stat. I pull the selected team using another FILTER, with C2 again being the name of the team:
```
=FILTER($G$2:$G,$B$2:$B=Matchup!$C$2)
```
It then uses a similar INDIRECT formula to pull the speed for the right format. To the right, I use a SORT formula to sort them by Speed. This is what powers the section in the middle of the "Home" tab that shows the Pokemon sorted by Speed.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/c8ab804f-0874-4025-b09b-9913d1855227)

In order for the "Matchup" tab to work properly, I had to use a slightly complicated QUERY formula, which basically works just like a SQL query.
```
=IFNA(QUERY(Backend!$B$2:$X,"Select L,M,N,O,P,Q,R,S,T,U,V,W,X
Where B ='"&$C$2&"' and not L is null
Order by "&IF(SortBy="Team Order","D asc",IF(SortBy="Alphabetical","L asc",IF(SortBy="Base Stats","O desc",IF(SortBy="HP","P desc",IF(SortBy="Attack","Q desc",IF(SortBy="Defense","R desc",IF(SortBy="Sp. Attack","S desc",IF(SortBy="Sp. Defense","T desc",IF(SortBy="Speed","U desc","D"))))))))),0),"")
```
- It starts by selecting all of the specific columns with the necessary data, but only if column B (which shows the selected team) matches with the selected team from the above toggle located in cell C2 (Where B ='"&$C$2&"').
- It then ensures it only has cells that have text within them (and not L is null), so that it does not cause issues with sorting.
- Lastly, it uses Order By with many different criteria, used with IF statements within Google Sheets. For example, if Speed is toggled on the "Sort By" dropdown, it sorts the selected rows by column U on the Backend tab.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/eab48f02-af6b-4b11-97b5-284f369d076b)

For the Type Matchup section, I use IF formulas to look at the specific Pokemon's typing and abilities in order to determine how effective the specific type would be against it. For example, this formula shows effectiveness against the Water type:
```
=IF($G4="","",IF(COUNTIF(G4:H4,"Ground")>0,2,1)*IF(COUNTIF(G4:H4,"Rock")>0,2,1)*IF(COUNTIF(G4:H4,"Fire")>0,2,1)*IF(COUNTIF(G4:H4,"Water")>0,0.5,1)*IF(COUNTIF(G4:H4,"Grass")>0,0.5,1)*IF(COUNTIF(G4:H4,"Dragon")>0,0.5,1)*IF(COUNTIF(P4:R4,"Dry Skin")>0,0,1)*IF(COUNTIF(P4:R4,"Storm Drain")>0,0,1)*IF(COUNTIF(P4:R4,"Water Absorb")>0,0,1))
```
The formula first checks if there is a Pokemon. If not, it leaves the cell blank in order to avoid errors. It then checks if the Pokemon is a Ground type. If it is, it puts the number 2, as Ground takes double damage from Water. If not, it stays as 1. It then multiplies throughout the other checks. For example, if the selected Pokemon is Water/Ground type, it would multiply the 2 from Ground and the 0.5 from Water, making its effectiveness 1. If it also has the ability "Water Absorb", it would be multiplied by 0, making the effectiveness 0, since the Water Absorb ability blocks all Water-type damage.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/58c9ac2a-d392-4663-860f-74909f555f84)

Lastly, the "Moves" tab. Like Pokemon's stats, the moves they can learn are vastly different throughout each game and format, so this uses the same individual format tabs. All of the information from these tabs were pulled from public databases and websites, and the data is directly from the video games.

Basically, these tabs use formulas to see if the Pokemon's name on the right matches any of the selected team's Pokemon. If it does, it puts an X, as seen with Blissey, which is on the opposing team. The Moves tab then uses FILTER functions along with INDIRECT to search for all of the Pokemon that have an "X" next to them within the proper format.

There are many small features included that I did not mention simply because there is so much packed into this resource, but I covered all of the major features and how they work using backend code and functions. If you want to take a look at the resource yourself, I have attached a link in the introduction.
