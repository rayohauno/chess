.. chess_web_page documentation master file, created by
   sphinx-quickstart on Tue Jul 19 09:21:37 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Documentation for the *chess dataset*
=====================================

Original dataset
----------------

Here, we provide the chess dataset in two convenient formats (see below). However, if you are interested, you can download the original dataset from [1]_. The original dataset is stored in an efficient (in terms of space and access speed) but weird format that cannot be easily transformed into `PGN (Portable Game Notation) <https://en.wikipedia.org/wiki/Portable_Game_Notation>`_ format without using some specific program. If you want to work with the original data, anyway, I recommend you to install the chessDB software [1]_ that allows you to download the original data and then transform it to PGN format.

Description of the dataset and data curation
--------------------------------------------

In the original dataset there are around **3.5 million games**. If you study the cumulative number of games played as a function of time (following plot)

.. _N_vs_t:

.. figure:: _static/number_of_games_vs_time.png
           
you can see that the oldest game in the database is from the year 1783 (`a blindfold by Philidor <http://www.chessgames.com/perl/chessgame?gid=1440134>`_). After that, several periods can be appreciated, roughly. The first period consisting in old games where the data is very sparse. The second period, starting at the end of 1800, is when chess became a popular game. A third period occurs around 1960 during the cold war, when chess became a serious matter; i.e. it became a highly competitive and profesional sport. Finally, a fourth period starts around 1998 with the masification of the Internet. This last period contains most of the games and is the most consistent one. After filtered out games without a complete date (day,month,year), around **1.4 million games** remains. This is the dataset we used for the calculations in our papers [2]_ [3]_ [4]_. A similar dataset has been used in [5]_.

For more information about the dataset, please read the papers [2]_ [3]_ [4]_.

Download the dataset
--------------------

We provide the following files, each of which contains all and the same information but in different formats,

    All games in the original dataset transformed to .PGN format
    
        `all.pgn.zip <https://drive.google.com/file/d/0Bw0y3jV73lx_NElnLWVlNG9KNkU/edit?usp=sharing>`_  [831 MB]
        
    All games in a **simplified format** (created by us) with labels for easy filtering of games according to their attributes
    
        `all_with_filtered_annotations.txt.zip <https://drive.google.com/file/d/0Bw0y3jV73lx_aXE3RnhmeE5Rb1E/edit?usp=sharing>`_  [747 MB]

Description of the simplified format
------------------------------------

We converted the data in PGN format to a **simplified format** which we find convenient to work with. This format can be easily handled with a combination of different linux bash commands. Below we provide a few examples on how to do this but, first, let us describe the **simplified format**.

In the file ``all_with_filtered_annotations.txt``, lines starting with the character ``#`` correspond to comments or the description of the columns. For example::

the first 8 first lines of this file looks like. The last 3 lines correspond to the first 3 games in the file::

    # #
    # datetime 2013-08-10 22:32:16.640552
    # program programs/formats/pgn_to_filtered_very_basic_format_plus_info_filtering_info.py
    # filein original_data/scidbase/all.pgn
    # 1.t 2.date 3.result 4.welo 5.belo 6.len 7.date_c 8.resu_c 9.welo_c 10.belo_c 11.edate_c 12.setup 13.fen 14.resu2_c 15.oyrange 16.bad_len 17.game...
    1 2000.03.14 1-0 2851 None 67 date_false result_false welo_false belo_true edate_true setup_false fen_false result2_false oyrange_false blen_false ### W1.d4 B1.d5 W2.c4 B2.e6 W3.Nc3 B3.Nf6 W4.cxd5 B4.exd5 W5.Bg5 B5.Be7 W6.e3 B6.Ne4 W7.Bxe7 B7.Nxc3 W8.Bxd8 B8.Nxd1 W9.Bxc7 B9.Nxb2 W10.Rb1 B10.Nc4 W11.Bxc4 B11.dxc4 W12.Ne2 B12.O-O W13.Nc3 B13.b6 W14.d5 B14.Na6 W15.Bd6 B15.Rd8 W16.Ba3 B16.Bb7 W17.e4 B17.f6 W18.Ke2 B18.Nc7 W19.Rhd1 B19.Ba6 W20.Ke3 B20.Kf7 W21.g4 B21.g5 W22.h4 B22.h6 W23.Rh1 B23.Re8 W24.f3 B24.Bb7 W25.hxg5 B25.fxg5 W26.d6 B26.Nd5+ W27.Nxd5 B27.Bxd5 W28.Rxh6 B28.c3 W29.d7 B29.Re6 W30.Rh7+ B30.Kg8 W31.Rbh1 B31.Bc6 W32.Rh8+ B32.Kf7 W33.Rxa8 B33.Bxd7 W34.Rh7+ 
    2 2000.03.14 1-0 2851 None 53 date_false result_false welo_false belo_true edate_true setup_false fen_false result2_false oyrange_false blen_false ### W1.e4 B1.d5 W2.exd5 B2.Qxd5 W3.Nc3 B3.Qa5 W4.d4 B4.Nf6 W5.Nf3 B5.c6 W6.Ne5 B6.Bf5 W7.g4 B7.Be4 W8.f3 B8.Bd5 W9.a3 B9.Nbd7 W10.Be3 B10.Nxe5 W11.dxe5 B11.Nxg4 W12.Bd4 B12.e6 W13.b4 B13.Qd8 W14.Nxd5 B14.Qxd5 W15.c4 B15.Ne3 W16.cxd5 B16.Nxd1 W17.dxc6 B17.bxc6 W18.Rxd1 B18.Be7 W19.Ba6 B19.O-O W20.Ke2 B20.Rab8 W21.Rc1 B21.Rfd8 W22.Rhd1 B22.c5 W23.Bxc5 B23.Rxd1 W24.Rxd1 B24.Bxc5 W25.bxc5 B25.g6 W26.c6 B26.Rb2+ W27.Rd2 
    3 1999.11.20 1-0 2851 None 57 date_false result_false welo_false belo_true edate_false setup_false fen_false result2_false oyrange_false blen_false ### W1.e4 B1.e5 W2.Nf3 B2.Nc6 W3.Bc4 B3.Bc5 W4.c3 B4.Nf6 W5.d3 B5.d6 W6.Bb3 B6.O-O W7.Nbd2 B7.Be6 W8.O-O B8.Qd7 W9.Re1 B9.Rfe8 W10.Nf1 B10.Ne7 W11.Ng3 B11.Bg4 W12.h3 B12.Be6 W13.Bg5 B13.Kh8 W14.Bxf6 B14.gxf6 W15.d4 B15.exd4 W16.cxd4 B16.Bb4 W17.Re3 B17.Rg8 W18.d5 B18.Bxh3 W19.Qd4 B19.Rg6 W20.Qxb4 B20.c5 W21.Qc3 B21.Bg4 W22.Bc2 B22.Rh6 W23.Nh2 B23.b5 W24.b4 B24.Rc8 W25.Bd3 B25.c4 W26.Bc2 B26.Bh5 W27.Nxh5 B27.Rxh5 W28.Qxf6+ B28.Kg8 W29.Bd1 

After the comments and description of the columns, each line corresponds to one and only one game. The first columns describe attributes of the game, such as the date in which it was played, the name of the players, etc. The last columns, from 17 onwards after the token ``###``, contains the sequence of the game moves. Let us provide a description for the columns of the game attributes:

1. Position of the game in the original PGN file. 
    
2. Date at which the game was played (the format is ``year.month.day``).
    
3. Game result specified inside brackets in the PGN file. The value can be ``1``, ``0`` or ``-1`` corresponding to white win, draw or loose, respectively.
    
4. `ELO <https://en.wikipedia.org/wiki/Elo_rating_system>`_ of withe player (an integer number).
    
5. ELO of black player (an integer number).
    
6. Number of moves in the game (for some games it may be zero!)
    
7. ``date_c`` = date (in ``year.month.day``) is corrupted or missing? the label should be ``date_true``, meaning the date is corrupted, or ``date_false``, meaning the date is NOT corrupted. The same logic applies to the following attributes ending in "_c" (i.e. _corrupted).
    
8. ``resu_c`` = result (``1-0``, ``1/2-1/2``, or ``0-1``) is corrupted or missing?
    
9. ``welo_c`` = withe ELO is corrupted or missing? 
    
10. ``belo_c`` = black ELO is corrupted or missing?
    
11. ``edate_c`` = event date is corrupted or missing? The event where the game was held (if there is one).
    
12. ``setup`` may be ``setup_true`` or ``setup_false``. If it is true then the game initial position is specified. This is used when playing Fischer Random Chess for example.
    
13. ``fen`` may be ``fen_true`` and ``fen_false``. It is related to column 12.
    
14. In the original file the result is provided in two places. At the end of each sequence of moves and in the attributes part. This flag indicates if the result is (is not) properly provided after the sequence of moves (just for checking consistency in the PGN file).
    
15. ``oyrange`` may be ``oyrange_true`` or ``oyrange_false``. This flag is false only for games with dates in the range of years [1998,2007]. The ``oyrange`` means ``out of year range``.
    
16. ``bad_len`` (or bad len) flag indicates, when ``blen_true`` (``blen_false``), if the length of the game is (is not) good.
    
17. Finally, after the token ``###``, you can find the sequence of moves. Each move has a number and a letter ``W`` (white) or ``B`` (black) indicating the th-move of the white or black player, respectively. 

The sequence of moves for one game (the first game in the dataset, in this case) looks as follows::

    W1.d4 B1.d5 W2.c4 B2.e6 W3.Nc3 B3.Nf6 W4.cxd5 B4.exd5 W5.Bg5 B5.Be7 W6.e3 B6.Ne4 W7.Bxe7 B7.Nxc3 W8.Bxd8 B8.Nxd1 W9.Bxc7 B9.Nxb2 W10.Rb1 B10.Nc4 W11.Bxc4 B11.dxc4 W12.Ne2 B12.O-O W13.Nc3 B13.b6 W14.d5 B14.Na6 W15.Bd6 B15.Rd8 W16.Ba3 B16.Bb7 W17.e4 B17.f6 W18.Ke2 B18.Nc7 W19.Rhd1 B19.Ba6 W20.Ke3 B20.Kf7 W21.g4 B21.g5 W22.h4 B22.h6 W23.Rh1 B23.Re8 W24.f3 B24.Bb7 W25.hxg5 B25.fxg5 W26.d6 B26.Nd5+ W27.Nxd5 B27.Bxd5 W28.Rxh6 B28.c3 W29.d7 B29.Re6 W30.Rh7+ B30.Kg8 W31.Rbh1 B31.Bc6 W32.Rh8+ B32.Kf7 W33.Rxa8 B33.Bxd7 W34.Rh7+

This is the string that should be parsed, e.g. using Python, to process the first game on the **simplified format** of the database.

**IMPORTANT**: In the file ``all_with_filtered_annotations.txt`` the games are NOT in chronological order because some games have missing date in the original database.

Easy filtering of undesired games and sorting by date: examples using `bash <https://en.wikipedia.org/wiki/Bash_(Unix_shell)>`_ commands
-----------------------------------------------------------------------------------------------------------------------------------------

You can use a simple linux(bash) command to quickly filter games with undesired properties from this file. For instance, the command::

    cat all_with_filtered_annotations.txt | grep 'welo_false' > all_with_filtered_annotations_with_wELO.txt

will generate the file "all_with_filtered_annotations_with_wELO.txt" with games where the white ELO is provided. Of course you can concatenate the command ``greep`` to filter more than one property. For instance::

    cat all_with_filtered_annotations.txt | grep 'welo_false' | grep 'belo_false' > all_with_filtered_annotations_with_wELO_and_bELO.txt

will kept the games with both, white and black ELO specified. Another example,::

    cat all_with_filtered_anotations.txt | grep 'oyrange_false' > all_with_filtered_annotations_since1998.txt

will generate a file with games after the year 1998.

If you want to sort games by date, first generate a file filtering games with corrupted date by::

    cat all_with_filtered_anotations.txt | grep 'date_false' > all_with_filtered_annotations_with_dates.txt

and then use the following linux command to sort the games by date::

    sort -k2 all_with_filtered_annotations_with_dates.txt > all_with_filtered_annotations_sorted_by_date.txt

References
----------

.. [1] http://chessdb.sourceforge.net/

.. [2] Memory Kernel in the Expertise of Chess Players, A.L. Schaigorodsky, J.I. Perotti, O.V. Billoni, submitted (2015) `arXiv:1504.06611 <http://arxiv.org/abs/1504.06611>`_

.. [3] Memory and long range correlations in chess games, A.L. Schaigorodsky, J.I. Perotti, O.V. Billoni, Phys. A 394, 304-311 (2013) `arXiv:1307.0729 <http://arxiv.org/abs/1307.0729>`_

.. [4] Innovation and Nested Preferential Growth in Chess Playing Behavior, J.I. Perotti, H.-H. Jo, A.L. Schaigorodsky, O.V. Billoni, Europhys. Lett. 104, 48005 (2013) `arXiv:1309.0336 <http://arxiv.org/abs/1309.0336>`_

.. [5] Bernd Blasius and Ralf Tonjes. Zipfs law in the popularity distribution of chess openings. Phys. Rev. Lett., 103, 21, 218701 (2009) `APS <http://journals.aps.org/prl/abstract/10.1103/PhysRevLett.103.218701>`_.

.. Contents:

.. 
   .. toctree::
       :maxdepth: 2

..
    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`
