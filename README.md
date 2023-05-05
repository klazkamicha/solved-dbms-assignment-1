Download Link: https://assignmentchef.com/product/solved-dbms-assignment-1
<br>
<ul>

 <li>General Instructions

  <ol>

   <li>Please complete this assignment individually, on your own.</li>

   <li>You will submit 2 files: query.sql and EntryNumber.pdf, corresponding to the queries and a timings report, respectively.</li>

   <li>Use PostgreSQL 13 for your homework. See <a href="https://www.postgresql.org/download/">this link</a> for instructions on how to download and install it on your OS. The .sql files are run automatically using the psql command using the i option, so please ensure that there are no syntax errors in the file. If we are unable to run your file, you get an automatic reduction to 0 marks. To understand how to run many queries at once from text file, a dummy query file <a href="https://drive.google.com/file/d/1IH8zYTSiEYQFZZRnUF20RE_zouapPuon/view?usp=sharing">sql</a> is available. To run example.sql in PostgreSQL, type the following command in the terminal: sudo -u postgres psql dbname</li>

  </ol></li>

</ul>

i /address/to/example.sql

This command will run all the queries listed in example.sql at once.

<ol start="4">

 <li>The format of the file should be as follows. One line should identify the query number (note the two hyphens before and after the query number), followed by the actual, syntactically correct SQL query. Leave a blank line after each query.

  <ul>

   <li>-1- –</li>

  </ul></li>

</ol>

SQL QUERY

<ul>

 <li>-2- –</li>

</ul>

SQL QUERY

<ul>

 <li>-3- –</li>

</ul>

SQL QUERY

<ol start="5">

 <li>All of the queries below require an ’ORDER BY’ clause. If you made an error in this clause, your answer will be evaluated as incorrect and zero marks will be awarded.</li>

 <li>No changes are allowed in the i) data, ii) attribute names, iii) table names</li>

 <li>The .pdf file should contain a bar graph. The graph should report the timings for each query of the dataset (X-axis legend is the query number, Y-axis legend is the time taken). You will need to figure out how to measure the timings.</li>

 <li>The submission will be done on Moodle.</li>

 <li>If unspecified, order the result in ascending order by column 1, then column 2 .. etc. In case of any doubts please ask on Piazza. The instructors ordering will be final and no queries will be entertained on the same.</li>

 <li>In case any query or sub-query results in NULL values, please discard them before proceeding for any further steps. This is extremely important for some queries which ask us to list TOP n results etc, since you might get erroneous results.</li>

 <li>For all queries leading to floating point numbers, round off the number to two decimal places right when the number is computed (and not just at the end). Even a 0.01 error will result in a wrong answer.</li>

</ol>

<ul>

 <li>Dataset</li>

</ul>

<h1>2.1       Instructions</h1>

<ol>

 <li>In this assignment you will analyze IPL data from the years 2008-2016. The analysis has to be done in postgres. We are providing you cleaned up data and you can download it from <a href="https://drive.google.com/file/d/1AcodC5xnrJdV0Ca6YrBP_li0ShzVs9wg/view?usp=sharing">this </a> The zip file contains a comma- seperated (,) file for each table described below.(Note the order of values in file is same as attributes of table given in next bullet point). You can load the table into database from csv file using the command</li>

</ol>

copy Table-Name from ’/path/to/file/table-name.csv’ DELIMITER ’,’ CSV HEADER;

<ol start="2">

 <li>The database will include following fifteen tables and you should use only these tables while writing solution of the queries. All red coloured values are the primary keys across all tables. Note – you don’t have to define these tables in the submission file, these will already be present will evaluation. (a) Table player</li>

</ol>

<table width="385">

 <tbody>

  <tr>

   <td width="134">player_id:bigint</td>

   <td width="132">player_name:text</td>

   <td width="119">dob:timestamp</td>

  </tr>

  <tr>

   <td width="134">batting_hand:bigint</td>

   <td width="132">bowling_skill:bigint</td>

   <td width="119">country_id:bigint</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table match</li>

</ul>

<table width="436">

 <tbody>

  <tr>

   <td width="174">match_id:bigint</td>

   <td width="123">team_1:bigint</td>

   <td width="138">team_2:bigint</td>

  </tr>

  <tr>

   <td width="174">match_date:timestamp</td>

   <td width="123">season_id:bigint</td>

   <td width="138">win_id:bigint</td>

  </tr>

  <tr>

   <td width="174">win_margin:bigint</td>

   <td width="123">outcome_id:bigint</td>

   <td width="138">match_winner:bigint</td>

  </tr>

  <tr>

   <td width="174">man_of_the_match:bigint</td>

   <td width="123"> </td>

   <td width="138"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table player_match</li>

</ul>

<table width="316">

 <tbody>

  <tr>

   <td width="110">match_id:bigint</td>

   <td width="110">player_id:bigint</td>

   <td width="96">role_id:bigint</td>

  </tr>

  <tr>

   <td width="110">team_id:bigint</td>

   <td width="110"> </td>

   <td width="96"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table ball_by_ball</li>

</ul>

<table width="471">

 <tbody>

  <tr>

   <td width="199">match_id:bigint</td>

   <td width="134">over_id:bigint</td>

   <td width="137">ball_id:bigint</td>

  </tr>

  <tr>

   <td width="199">innings_no:bigint</td>

   <td width="134">team_batting:bigint</td>

   <td width="137">team_bowling:bigint</td>

  </tr>

  <tr>

   <td width="199">striker_batting_position:bigint</td>

   <td width="134">striker:bigint</td>

   <td width="137">non_striker:bigint</td>

  </tr>

  <tr>

   <td width="199">bowler:bigint</td>

   <td width="134"> </td>

   <td width="137"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table batsman_scored</li>

</ul>

<table width="340">

 <tbody>

  <tr>

   <td width="125">match_id:bigint</td>

   <td width="119">over_id:bigint</td>

   <td width="96">ball_id:bigint</td>

  </tr>

  <tr>

   <td width="125">runs_scored:bigint</td>

   <td width="119">innings_no:bigint</td>

   <td width="96"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table wicket_taken</li>

</ul>

<table width="323">

 <tbody>

  <tr>

   <td width="119">match_id:bigint</td>

   <td width="108">over_id:bigint</td>

   <td width="96">ball_id:bigint</td>

  </tr>

  <tr>

   <td width="119">player_out:bigint</td>

   <td width="108">kind_out:bigint</td>

   <td width="96">fielders:bigint</td>

  </tr>

  <tr>

   <td width="119">innings_no:bigint</td>

   <td width="108"> </td>

   <td width="96"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table season</li>

</ul>

<table width="412">

 <tbody>

  <tr>

   <td width="120">season_id:bigint</td>

   <td width="170">man_of_the_series:bigint</td>

   <td width="122">orange_cap:bigint</td>

  </tr>

  <tr>

   <td width="120">purple_cap:bigint</td>

   <td width="170">season_year:bigint</td>

   <td width="122"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table win_by</li>

</ul>

<table width="199">

 <tbody>

  <tr>

   <td width="100">win_id:bigint</td>

   <td width="99">win_type:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table team</li>

</ul>

<table width="221">

 <tbody>

  <tr>

   <td width="108">team_id:bigint</td>

   <td width="113">team_name:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table role</li>

</ul>

<table width="200">

 <tbody>

  <tr>

   <td width="100">role_id:bigint</td>

   <td width="99">role_desc:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table country</li>

</ul>

<table width="252">

 <tbody>

  <tr>

   <td width="123">country_id:bigint</td>

   <td width="128">country_name:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table outcome</li>

</ul>

<table width="255">

 <tbody>

  <tr>

   <td width="128">outcome_id:bigint</td>

   <td width="127">outcome_type:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table out_type</li>

</ul>

<table width="202">

 <tbody>

  <tr>

   <td width="98">out_id:bigint</td>

   <td width="103">out_name:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table bowling_style</li>

</ul>

<table width="245">

 <tbody>

  <tr>

   <td width="123">bowling_id:bigint</td>

   <td width="123">bowling_skill:text</td>

  </tr>

  <tr>

   <td width="123"> </td>

   <td width="123"> </td>

  </tr>

  <tr>

   <td width="123">batting_id:bigint</td>

   <td width="123">batting_hand:text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Table batting_style</li>

</ul>

2.2        Points for help:

<ul>

 <li>Every match has two Innings.</li>

 <li>Each team has 11 players in a match.</li>

 <li>In a match, a team is said to be chasing if that team is batting in the second innings.</li>

 <li>A wicket is considered to be taken by the bowler if and only if the out type is one of the following: Caught, Bowled, LBW, Stumped, Caught and Bowled, Hit Wicket.</li>

 <li>Purple cap is awarded to player who took most number of wickets in that season.</li>

 <li>Orange cap is awarded to player who is the leading run-scorer of that season.</li>

 <li>4, 6 runs are considered as boundaries.</li>

 <li>A fielder will be associated with a fall of wicket when the wicket type is as follows: Caught, Run out, Stumped.</li>

 <li>Batting average of a player is given by total runs scored by the batsman divided by number of matches played.</li>

 <li>A bowler B (say) is said to be conceded X runs (say) if batsmen have scored X runs with B as the bowler.</li>

</ul>

<h1>2.3      Queries</h1>

<ol>

 <li>Return the bowlers that took 5 or more wickets in a single match. sort in descending order of num_wickets. Break ties by ascending order by player_name and then team_name. Columns: match_id, player_name, team_name, num_wickets.</li>

 <li>Top 3 (all of them if count is less than 3) players who won most Man-of-the-matches being in a losing team. Sort in descending order of num_matches. Break ties with ascending (lexicographical) order of player names. Columns: Player_name, num_matches.</li>

 <li>Return the player who took most number of catches (as a fielder) in the year 2012. Break ties by ascending (lexicographical) order of player names. Columns: player_name.</li>

 <li>Return number of matches played by the purple cap player in that respective season. Sort in ascending order of season year. Columns: season_year, player_name, num_matches.</li>

 <li>Return the players who scored more than 50 runs in the matches their team lost. Sort in ascending (lexicographical) of player names. Columns: player_name.</li>

 <li>Return top 5 teams with most left handed foreign batsmen in each season. Sort in ascending order of season year. Break ties of number of such batsmen by ascending (lexicographical) order of team names in a season. Columns: season_year, team_name, rank.</li>

 <li>Return the teams in the order of maximum match wins in the season 2009. Break ties by ascending (lexicographical) order of team names. Columns: team_name</li>

</ol>

Note: consider the match_winner column of table match to decide the winner and take care of null values.

<ol start="8">

 <li>Return the top run scorer of each team in the year, 2010. Sort in the ascending order of team names. Break ties between players in the ascending order of player names. Columns: team_name, player_name, runs.</li>

 <li>Return top 3 teams with maximum number of sixes (runs_scored is 6 in batsman_scored) in a single innings in the season 2008. Break ties by ascending order of team names. Columns: team_name, opponent_team_name, number of sixes</li>

 <li>Return players with maximum batting average who took more wickets than an average bowler in each bowling category in all the seasons (Consider all matches of all seasons). Sort in ascending order of bowling_skill. Break ties in ascending order of player_name. Columns: bowling_category, player_name, batting_average.</li>

 <li>Return all the left handed batsmen who scored 150 or more runs and took 5 or more wickets and played 10 or more matches in a season. Sort in descending order of number of wickets, descending order of runs in the season. Break ties by ascending order of player names. Columns: season_year, player_name, num_wickets, runs.</li>

 <li>Find the season, match id,player name,team name and number of wickets where the highest number of wickets taken by a player in a match. Sort in descending order of number of wickets. Break ties by ascending order of player name, ascending order of match_id. Columns: match_id, player_name, team_name, num_wickets, season_year</li>

 <li>Return all the players who played in all the seasons. Sort in order of ascending order of player names. Columns: player_name.</li>

 <li>Return top 3 teams for each season based on number of batsmen with a score of 50 or more in a match they won. Sort in ascending order of season year and rank the teams in descending order of number of batsmen with a score of 50+. Break ties by ascending order of team names. Columns: season_year, match_id, team_name</li>

 <li>Return Players with second highest runs, second highest wickets along with the number of runs and wickets for each season. Sort in ascending order of season year. Break ties by ascending order of player names for both batsmen and bowlers while ranking. Columns: season_year, top_batsman, max_runs, top_bowler, max_wickets</li>

 <li>Find all teams against which ’Royal Challengers Bangalore’ lost a match in 2008. Sort in descending order of number of matches won against ’Royal Challengers Bangalore’ in 2008. Break ties by ascending order of team name. Columns: team_name.</li>

 <li>For each team, return the player who has been awarded man of the match maximum number of times. Sort in order of ascending order of team names. Break ties by ascending order of player name while ranking. Columns: team_name, player_name, count.</li>

 <li>Return top 5 players who played in 3 or more teams and have conceded more than 20 runs in an over for the most number of times. Break ties by ascending order of player names. Columns: player_name.</li>

 <li>Return average runs of each team in season 2010, rounded off to 2 decimals. (Ignore the extras). Sort in ascending order of team name. Columns: team_name, avg_runs.</li>

 <li>Return top 10 players who got out in the first over (of the match) for most number of times.</li>

</ol>

Break ties by ascending order of player names. Columns: player_names.

<ol start="21">

 <li>Return top 3 matches where team wins by chasing with least number of boundaries. Sort in ascending order of number of boundaries. Break ties by ascending order of match_winner team name, team_1 name, team_2 name. Columns: Match_id, team_1_name, team_2_name, match_winner_name, number_of_boundaries.</li>

 <li>Return the countries of top 3 players with lowest average runs conceded per number of wickets taken over all matches. Break ties by ascending order of player name. Discard players with 0 total wickets. Columns: country_name.</li>

</ol>