-- Drop existing tables
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE Registration CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Venue CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Catering CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Theme CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Clients CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Guest_Groom CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Guest_Bride CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Task CASCADE CONSTRAINTS';
    EXECUTE IMMEDIATE 'DROP TABLE Employee CASCADE CONSTRAINTS';
EXCEPTION
    WHEN OTHERS THEN
        NULL;
END;
/

-- Create Catering table
CREATE TABLE Catering (
    cid VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    price NUMBER(10, 2) NOT NULL,
    PRIMARY KEY (cid)
);

-- Create Clients table
CREATE TABLE Clients (
    pid VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    email VARCHAR2(30) NOT NULL,
    phone VARCHAR2(20) NOT NULL,
    PRIMARY KEY (pid)
);

-- Create Theme table
CREATE TABLE Theme (
    tid VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    price NUMBER(10, 2) NOT NULL,
    PRIMARY KEY (tid)
);

-- Create Venue table
CREATE TABLE Venue (
    vid VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    price NUMBER(10, 2) NOT NULL,
    PRIMARY KEY (vid)
);

-- Create Employee table
CREATE TABLE Employee (
    emp_id VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    role VARCHAR2(30) NOT NULL,
    contact_info VARCHAR2(50),
    PRIMARY KEY (emp_id)
);

-- Create Registration table with foreign keys
CREATE TABLE Registration (
    reg_id VARCHAR2(10) NOT NULL,
    wdate DATE NOT NULL,
    vid VARCHAR2(10) NOT NULL,
    cid VARCHAR2(10) NOT NULL,
    tid VARCHAR2(10) NOT NULL,
    pid VARCHAR2(10) NOT NULL,
    PRIMARY KEY (reg_id),
    FOREIGN KEY (vid) REFERENCES Venue(vid),
    FOREIGN KEY (cid) REFERENCES Catering(cid),
    FOREIGN KEY (tid) REFERENCES Theme(tid),
    FOREIGN KEY (pid) REFERENCES Clients(pid)
);

-- Create Guest_Groom table
CREATE TABLE Guest_Groom (
    groom_id VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    phone VARCHAR2(20) NOT NULL,
    PRIMARY KEY (groom_id)
);

-- Create Guest_Bride table
CREATE TABLE Guest_Bride (
    bride_id VARCHAR2(10) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    phone VARCHAR2(20) NOT NULL,
    PRIMARY KEY (bride_id)
);

-- Create Task table
CREATE TABLE Task (
    task_id VARCHAR2(10) NOT NULL,
    task_name VARCHAR2(100) NOT NULL,
    description VARCHAR2(255),
    assigned_to VARCHAR2(10) NOT NULL,
    deadline DATE,
    status VARCHAR2(20),
    PRIMARY KEY (task_id),
    FOREIGN KEY (assigned_to) REFERENCES Employee(emp_id)
);

-- Insert values into Clients table
INSERT INTO Clients (pid, name, email, phone) 
VALUES ('P1', 'John Doe', 'john.doe@example.com', '1234567890');
INSERT INTO Clients (pid, name, email, phone) 
VALUES ('P2', 'Jane Smith', 'jane.smith@example.com', '0987654321');
INSERT INTO Clients (pid, name, email, phone) 
VALUES ('P3', 'Arif Rahman', 'arif.rahman@example.com', '1122334455');
INSERT INTO Clients (pid, name, email, phone) 
VALUES ('P4', 'Shila Begum', 'shila.begum@example.com', '2233445566');

-- Insert values into Catering table
INSERT INTO Catering (cid, name, price) 
VALUES ('C1', 'Bengali Fish Curry', 1500);
INSERT INTO Catering (cid, name, price) 
VALUES ('C2', 'Shorshe Ilish', 2500);
INSERT INTO Catering (cid, name, price) 
VALUES ('C3', 'Chicken Rezala', 1800);
INSERT INTO Catering (cid, name, price) 
VALUES ('C4', 'Vegetarian Platter', 1000);

-- Insert values into Theme table
INSERT INTO Theme (tid, name, price) 
VALUES ('T1', 'Traditional Bengali', 8000);
INSERT INTO Theme (tid, name, price) 
VALUES ('T2', 'Modern Bengali', 12000);
INSERT INTO Theme (tid, name, price) 
VALUES ('T3', 'Royal Wedding', 15000);
INSERT INTO Theme (tid, name, price) 
VALUES ('T4', 'Vintage Wedding', 10000);

-- Insert values into Venue table
INSERT INTO Venue (vid, name, price) 
VALUES ('V1', 'Shonar Bangla Hall', 15000);
INSERT INTO Venue (vid, name, price) 
VALUES ('V2', 'Rabindra Sadan', 20000);
INSERT INTO Venue (vid, name, price) 
VALUES ('V3', 'Nazrul Mancha', 18000);
INSERT INTO Venue (vid, name, price) 
VALUES ('V4', 'Bangla Academy', 25000);

-- Insert values into Registration table
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R1', TO_DATE('2024-01-15', 'YYYY-MM-DD'), 'V1', 'C1', 'T1', 'P1');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R2', TO_DATE('2024-02-10', 'YYYY-MM-DD'), 'V2', 'C2', 'T2', 'P2');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R3', TO_DATE('2024-03-20', 'YYYY-MM-DD'), 'V3', 'C3', 'T3', 'P3');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R4', TO_DATE('2024-04-05', 'YYYY-MM-DD'), 'V4', 'C4', 'T4', 'P4');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R5', TO_DATE('2024-05-10', 'YYYY-MM-DD'), 'V1', 'C2', 'T2', 'P1');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R6', TO_DATE('2024-06-15', 'YYYY-MM-DD'), 'V2', 'C3', 'T1', 'P2');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R7', TO_DATE('2024-07-20', 'YYYY-MM-DD'), 'V3', 'C1', 'T3', 'P3');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R8', TO_DATE('2024-08-05', 'YYYY-MM-DD'), 'V4', 'C4', 'T4', 'P4');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R9', TO_DATE('2024-09-10', 'YYYY-MM-DD'), 'V1', 'C3', 'T3', 'P1');
INSERT INTO Registration (reg_id, wdate, vid, cid, tid, pid) VALUES ('R10', TO_DATE('2024-10-12', 'YYYY-MM-DD'), 'V2', 'C2', 'T4', 'P3');

-- Insert values into Guest_Groom table
INSERT INTO Guest_Groom (groom_id, name, phone) 
VALUES ('G1', 'Alice Brown', '9876543210');
INSERT INTO Guest_Groom (groom_id, name, phone) 
VALUES ('G2', 'Bob White', '9876554321');
INSERT INTO Guest_Groom (groom_id, name, phone) 
VALUES ('G3', 'Charlie Green', '9876609876');

-- Insert values into Guest_Bride table
INSERT INTO Guest_Bride (bride_id, name, phone) 
VALUES ('B1', 'Alice Brown', '9876543210');
INSERT INTO Guest_Bride (bride_id, name, phone) 
VALUES ('B2', 'David Blue', '9876610987');
INSERT INTO Guest_Bride (bride_id, name, phone) 
VALUES ('B3', 'Bob White', '9876554321');

-- Insert values into Employee table
INSERT INTO Employee (emp_id, name, role, contact_info) 
VALUES ('E1', 'David Clark', 'Event Planner', 'david@example.com');
INSERT INTO Employee (emp_id, name, role, contact_info) 
VALUES ('E2', 'Sophia Turner', 'Catering Manager', 'sophia@example.com');

-- Insert values into Task table
INSERT INTO Task (task_id, task_name, description, assigned_to, deadline, status) 
VALUES ('T1', 'Arrange Catering', 'Ensure food is ready and served', 'E2', TO_DATE('2024-01-14', 'YYYY-MM-DD'), 'Pending');
INSERT INTO Task (task_id, task_name, description, assigned_to, deadline, status) 
VALUES ('T2', 'Venue Decoration', 'Decorate venue with theme decor', 'E1', TO_DATE('2024-01-14', 'YYYY-MM-DD'), 'Pending');

-- Commit to save changes
COMMIT;

-- Display table contents
SELECT * FROM Catering;
SELECT * FROM Clients;
SELECT * FROM Theme;
SELECT * FROM Venue;
SELECT * FROM Registration;
SELECT * FROM Guest_Groom;
SELECT * FROM Guest_Bride;
SELECT * FROM Employee;
SELECT * FROM Task;
 
  
