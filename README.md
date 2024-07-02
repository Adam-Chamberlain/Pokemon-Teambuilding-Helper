# Pokemon Teambuilding Helper

## Introduction

Competitive Pokemon battling has been a hobby of mine for many years. There are many different ways to play the game, but my preferred way is to create a team of Pokemon and counter-team opposing teams. As a simplified example: I have a team of 8 Pokemon, and my opponent has 8 different ones. I must pick 6 of them and create a plan in order to defeat the opponent's team of 6. While it sounds simple, Pokemon actually has a lot of depth in it; each Pokemon can be used dozens of different ways, and their stats can be modified in order to more effectively counter opponents. This is a lot to handle, especially for newer players, and many people, myself included, enjoy visuals that lay out all of the important aspects within a matchup.

In early 2023, I decided to create this resource to help people in their teambuilding process. It started as a small project, but as time went on, more people began using it, and I added many different features to account for different ways people play the game. Now, it covers over 10 different formats, and an estimated 1,000+ people use the resource on a weekly basis.

This resource was made in Google Sheets, and it uses hundreds of long and complicated functions to be fully automated. I have spent hundreds of hours testing and modifying this resource to make it as effective and easy to use as possible for the people that use it.

## Brief Overview

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/3e89e38a-7be5-470e-8137-6008e33fdc70)

This is the "Home" page, which shows a quick overview graphic of a given matchup. The team selected is "Example", and the format is "National Dex", which means every Pokemon that exists, regardless of if it is available in the most recent video games.

Throughout the resource, blue represents the user's team, and red represents the opposing team. In the middle, the "Speed Tiers" show what each Pokemon's Speed stat is. This is important for users to know because faster Pokemon always attack before slower ones.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/6cabcc37-df5e-4fcd-875c-537f685f2107)

This is the "Teams" page, which is the only place data is manually inputted. This is where users put their teams and change the team name and format.

- "Cpt" stands for Captain, which are Pokemon that can use specific mechanics that exist in some games, such as the ability to change its type or gain a single-use move that does much more damage.
- In many scenarios, teams must be created on a budget, and Pokemon are priced based on how strong they are. The "Cost" column lets users easily calculate how many points they have remaining based on a specific budget.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/df6e9a19-c9dc-46a0-ab2f-d41284e938ea)

Here is the "Matchup" page, which has much more detailed information about a given matchup. This includes Pokemon's typings and abilities, which are all important traits to be aware of. It can also be sorted in many different ways, including by a specific stat (such as Speed), alphabetically, and the same order from the Teams page.

![image](https://github.com/Adam-Chamberlain/Pokemon-Teambuilding-Helper/assets/173857433/144f75dc-3dd9-4614-b307-87f70b367391)

Also on the Matchup page, this is a chart that shows how effective each type is against a given Pokemon. For example, Dugtrio at the top takes 0x damage from Electric attacks, but it takes 2x damage from Ice attacks.

- The last few rows are empty because the resource supports teams of up to 12 Pokemon, and this example only has teams of 8.
- "Count" shows how many Pokemon of a specific type are on the team. It's generally better to have a variety of types in order to not be very weak to specific types.
- "Weak" is a mathematical formula that shows about how weak the team is in total to a given type. For example, Rock is the biggest weakness on the top team because it has three Pokemon weak to it (two that take 2x damage and one that takes 4x damage) and only one that takes 0.5x damage from it. The full breakdown for how it's calculated is below:

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

The "Moves" page shows key moves that Pokemon on the team get. These moves are importan to take note of when creating a team and preparing against an opposing team. This tab has two modes: "Singles", which is 1 versus 1, and "Doubles", which is 2 versus 2. Different moves are relevant depending on the way people play, so the toggle shows different relevant moves.

## How it Works
