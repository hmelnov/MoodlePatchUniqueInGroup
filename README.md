# MoodlePatchUniqueInGroup
Unique question in group

When I have N questions for M students, N>M, I want to be able to give each student his own unique question using the random question in test.

After some googling I was convinced that Moodle doesn`t support the capability now.

But because of coronavirus and distance learning I was very much in need of this capability, so I have implemented it myself.

After reading Moodle code  I have found, that it already has a way to count how many times each question was given to the current student. To solve my problem I have modified the file

\mod\quiz\classes\question\qubaids_for_users_attempts.php

by adding the $uniqueingroup parameter. When $uniqueingroup is true it now counts the attempts of the other students passing the same test.

I have also changed some other PHP files to be able to edit, save and pass the $uniqueingroup attribute (total 7 files changed).

To avoid messing with the changes of the database structure I decided to combine the $uniqueingroup attribute with the $includesubcategories attribute. Now the field includingsubcategories of the table mdl_quiz_slots is considered as a combination of the bit flags
(0x1 - includesubcategories, 0x2 - uniqueingroup)
(it was 0..1 before, so the new code will correctly work with the existing database).

We have already tested the resulting changes on our students (educa.isu.ru), and the code works Ok.

I believe, that the unique in group capability will be useful for other teachers, who use Moodle.

The repository contains two folders:

New - the files, that were modified to support the "Unique in group" capability

Old - the state of the files before I have modified them (just in case that the files were modified for some other purposes since my editing)


