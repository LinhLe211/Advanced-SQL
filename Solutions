-- Excercise 1. JOIN
-- Question 1:List the school names, community names and average attendance for communities with a hardship index of 98.
SELECT CPS.NAME_OF_SCHOOL, CPS.COMMUNITY_AREA_NAME, CPS.AVERAGE_STUDENT_ATTENDANCE, CSD.HARDSHIP_INDEX 
FROM chicago_public_schools AS CPS 
INNER JOIN chicago_socioeconomic_data AS CSD 
ON CPS.COMMUNITY_AREA_NAME = CSD.COMMUNITY_AREA_NAME  
WHERE CSD.HARDSHIP_INDEX = 98;

-- Question 2: list all crimes that took place at a school. Include case number, crime type and community name.
SELECT 	CC.CASE_NUMBER, CC.PRIMARY_TYPE, CSD.COMMUNITY_AREA_NAME FROM chicago_crime AS CC LEFT OUTER JOIN chicago_socioeconomic_data AS CSD ON CC.COMMUNITY_AREA_NUMBER = CSD.COMMUNITY_AREA_NUMBER WHERE CC.LOCATION_DESCRIPTION LIKE '%SCHOOL%';

-- Excercise 2. VIEW
-- Question 1: Create a view:  
DROP VIEW IF EXISTS SCHOOL_NAME;
CREATE VIEW SCHOOL_NAME (School_Name,Safety_Rating, Family_Rating,Environment_Rating, Instruction_Rating,Leaders_Rating,Teachers_Rating) AS
SELECT NAME_OF_SCHOOL, Safety_Icon, Family_Involvement_Icon, Environment_Icon, Instruction_Icon, Leaders_Icon, Teachers_Icon FROM chicago_public_schools;

-- Question 2: Returns all of the columns from the view.
SELECT * FROM SCHOOL_NAME;

-- Question 3: Returns just the school name and leaders rating from the view.
SELECT School_Name, Leaders_Rating FROM SCHOOL_NAME;

-- Excercise 3. STORED PROCEDURE
-- Question 1.Create or replace a stored procedure called UPDATE_LEADERS_SCORE that takes a in_School_ID parameter as an integer and a in_Leader_Score parameter as an integer:

DROP PROCEDURE IF EXISTS UPDATE_LEADERS_SCORE;

DELIMITER //

CREATE PROCEDURE UPDATE_LEADERS_SCORE (in_School_ID Int, in_Leader_Score Int)
BEGIN
	
END //

DELIMITER ;
-- Question 2. Update the Leaders_Score field in the CHICAGO_PUBLIC_SCHOOLS table for the school identified by in_School_ID to the value in the in_Leader_Score parameter inside your stored procedure.
DROP PROCEDURE IF EXISTS UPDATE_LEADERS_SCORE;

DELIMITER //

CREATE PROCEDURE UPDATE_LEADERS_SCORE (in_School_ID Int, in_Leader_Score Int)
BEGIN
 		UPDATE chicago_public_schools SET Leaders_Score = in_Leader_Score WHERE  School_ID = in_School_ID;
END//

DELIMITER ;

-- Question 3: Update the Leaders_Icon field in the CHICAGO_PUBLIC_SCHOOLS table for the school identified by in_School_ID in the stored procedure.

DROP PROCEDURE IF EXISTS UPDATE_LEADERS_SCORE;

DELIMITER //

CREATE PROCEDURE UPDATE_LEADERS_SCORE (in_School_ID INT, in_Leader_Score INT)
BEGIN
    -- Update Leaders_Score
    UPDATE chicago_public_schools 
    SET Leaders_Score = in_Leader_Score 
    WHERE School_ID = in_School_ID;

    -- Update Leaders_Icon based on the score
    IF in_Leader_Score > 0 AND in_Leader_Score < 20 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 40 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 60 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Average' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 80 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Strong' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 100 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Strong' 
        WHERE School_ID = in_School_ID;
    END IF;
	
END //

DELIMITER ;

-- Q4. Call the stored procedure with a valid school ID and leader score
-- Check initial values
SELECT School_ID, Leaders_Score, Leaders_Icon
FROM chicago_public_schools 
WHERE School_ID = 610038;

-- Execute the procedure
CALL UPDATE_LEADERS_SCORE(610038, 50);

-- Verify updates
SELECT School_ID, Leaders_Score, Leaders_Icon
FROM chicago_public_schools 
WHERE School_ID = 610038;

-- Exercise 4: TRANSACTION
-- Question 1: Update your stored procedure definition. Add a generic ELSE clause to the IF statement that rolls back the current work if the score did not fit any of the preceding categories.

DROP PROCEDURE IF EXISTS UPDATE_LEADERS_SCORE;

DELIMITER //

CREATE PROCEDURE UPDATE_LEADERS_SCORE (in_School_ID INT, in_Leader_Score INT)
BEGIN
    -- Update Leaders_Score
    UPDATE chicago_public_schools 
    SET Leaders_Score = in_Leader_Score 
    WHERE School_ID = in_School_ID;

    -- Update Leaders_Icon based on the score
    IF in_Leader_Score > 0 AND in_Leader_Score < 20 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 40 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 60 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Average' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 80 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Strong' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 100 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Strong' 
        WHERE School_ID = in_School_ID;
    ELSE 
        ROLLBACK WORK;
    END IF;
END //

DELIMITER ;

-- Question 2: Update your stored procedure definition again. Add a statement to commit the current unit of work at the end of the procedure.

DROP PROCEDURE IF EXISTS UPDATE_LEADERS_SCORE;

DELIMITER //

CREATE PROCEDURE UPDATE_LEADERS_SCORE (in_School_ID INT, in_Leader_Score INT)
BEGIN
    -- Update Leaders_Score
    UPDATE chicago_public_schools 
    SET Leaders_Score = in_Leader_Score 
    WHERE School_ID = in_School_ID;

    -- Update Leaders_Icon based on the score
    IF in_Leader_Score > 0 AND in_Leader_Score < 20 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 40 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Weak' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 60 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Average' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 80 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Strong' 
        WHERE School_ID = in_School_ID;

    ELSEIF in_Leader_Score < 100 THEN
        UPDATE chicago_public_schools 
        SET Leaders_Icon = 'Very Strong' 
        WHERE School_ID = in_School_ID;
    ELSE 
        ROLLBACK WORK;
    END IF;
COMMIT WORK;	
END //

DELIMITER ;
