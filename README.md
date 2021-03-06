# CSGOML
`CSGOML` is a collection of [python](https://www.python.org/downloads/) of scripts to do [CS:GO](https://store.steampowered.com/app/730/CounterStrike_Global_Offensive/?l=german) data analysis utilizing the [awpy](https://github.com/pnxenopoulos/awpy) package for data parsing.

# demo_analyzer_sort.py
Contains a class automating the parsing of multi files in succession with awpy and sorting the resulting json files by map.

Useful when you have accumulated a large collection of your own demos and/or when doing map specific data analysis.

# fight_analyzer.py
Contains a class for analyzing a specifically defined engagement for whether it is T or CT favoured.

Running the script analyzes the early (first 5 to 25 seconds of the round) mid fight on inferno on gun rounds.

For that kill events are analyzed for their time, attacker and victim position and weaponry.

For each qualifying event an entry is made into a dataframe containing information about the time,round,matchid,killing weapon, winner and areas for further analysis.

The class natively supports checking the CT win percentage for different allowed time windows (One second steps from min to max. So just events between 5 and 6 seconds, 5 and 7, up to all 5 to 25).

# tensorflow_input_preparation.py
A script that produces, for each map separately, a json file containing different configurations of player trajectory data for each round played on that map. 

This is in perparation of further analysis to separate the extensive cleaning neccessary from the final analysis.

# read_tensorflow_input.py
Contains a class designed to read in the json files produced by tensorflow_input_preparation.py and train LSTM networks to predict a winner of a round based on player trajectory data. 

It supports the option to chose between which side(s) to consider, limit the data to only contain the first n seconds and to chose
between using each players full x, y and z coordinates or a tokenized version as described in [ggViz: Accelerating Large-Scale Esports Game Analysis](https://arxiv.org/pdf/2107.06495.pdf) and implemented in [awpy](https://github.com/pnxenopoulos/awpy).

# download_demos.py and demo_watchdog.py
Two scripts used to build a dataset large enough to enable machine learning techniques to fulfill their potential.

download_demos.py downloads the demos from professional CS:GO games tracked on [hltv](https://www.hltv.org/). 

demo_watchdog.py then unpacks the resulting rar file
and calls demo_analyzer_sort.py to parse the demos to json files and store them based on the map played. 

The full demos is subsequently deleted as hard disk requirement needed to store all demos in full us currently infeasible for me. 

Currently more than 1000 matches (>2000 maps with over 50000 rounds) have been accumulated.

# plot_utils.py

This is a module containing various functions that augments already existing plotting functions present in [awpy](https://github.com/pnxenopoulos/awpy).
Specifically the plotting of position tokens and visualization of named areas.
Run as a script it illustrates the basic functionality of these functions as well as the basic ones directly from awpy.
