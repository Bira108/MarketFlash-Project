-- Marketflash Project \-- Ubiratan Gonzaga e Silva \- DASep25

\-- Tables:

create table Clients (  
  Client\_id char (20) primary key,  
  Name varchar (20),  
  Address varchar (20),  
  email varchar (20),  
  phone varchar (20),  
  Contact\_person varchar (20)) ;

create table Campaigns (  
 Campaign\_id char (10) primary key,  
 Name varchar (20),  
 Start\_date date,  
 End\_date date,  
 Budget float,  
 Client\_id char (5),  
 foreign key (Client\_id) references Clients (Client\_id)) ;

create table Influencers (  
Influencer\_id char (10) primary key,  
Name varchar (50),  
Social\_handle varchar (30),  
Follower\_count int,  
Contact\_details varchar (250));

create table Campaign\_influencer (  
Campaign\_id char (10),  
Influencer\_id char (10),  
Primary key (Campaign\_id, Influencer\_id), \-- used as composite primary key  
foreign key (Campaign\_id) references Campaigns (Campaign\_id),  
foreign key (Influencer\_id) references Influencers (Influencer\_id));

create table Payments (  
  Payment\_id char (10),  
  Date date,  
  Amount float,  
  Payment\_type varchar (20),  
  Payment\_detail varchar (250),  
  Campaign\_id char (10),  
  primary key (Payment\_id)  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id)) ;  
create table Employees (  
  Employee\_id char (10) primary key,  
  Name varchar (10),  
  Role varchar (20),  
  Address varchar (50),  
  Department varchar (20),  
  Employee\_since date) ;

create table Campaign\_employees (  
  Campaign\_id char (10),  
  Employee\_id char (10),  
  primary key (Campaign\_id, Employee\_id),  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id),  
  foreign key (Employee\_id) references Employees (Employee\_id)) ;

create table Metrics (  
  Metric\_id char (10) primary key,  
  Impressions int,  
  Clicks int,  
  Engagement float,  
  Conversion\_rate float,  
  Campaign\_id char (10),  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id));

create table Contents (  
  Content\_id char (10) primary key,  
  Title varchar (20),  
  Description varchar (250),  
  Media\_type varchar (20),  
  Creation\_date date,  
  Campaign\_id char (10),  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id));

create table Plataforms (  
  Plataform\_id char (10) primary key,  
  Name varchar (20),  
  URL varchar (30),  
  Contact\_person string,  
  Contact\_phone varchar (20),  
  Contact\_email varchar (20));

create table Campaigns\_plataforms (  
  Campaign\_id char (10),  
  Plataform\_id char (10),  
  primary key (Campaign\_id, Plataform\_id),  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id),  
  foreign key (Plataform\_id) references Plataforms (Plataform\_id));

create table Advertisement (  
  Ad\_id char (10) primary key,  
  Ad\_name varchar (20),  
  Type varchar (20),  
  Duration float,  
  Budget float,  
  Campaign\_id char (10),  
  Plataform\_id char (10),  
  foreign key (Campaign\_id) references Campaigns (Campaign\_id)  
  foreign key (Plataform\_id) references Plataforms (Plataform\_id));

    
\-- Insert five entries in each table \--

insert into Clients (Client\_id, Name, Address, email, phone, Contact\_person)  
values  
  ('C001', 'Lopez PLC', '0806 Watson Drive Suite 662, Port Andrea, DE', 'zmcintyre@bauer.info', '3724028579', 'Barbara Walker'),  
  ('C002', 'Weaver, Garner and Ramos', '2933 Ortiz Overpass Suite 099, South Douglasburgh, KY' , 'oscott@gmail.com', '498.978.7718', 'Melinda Johnston'),  
  ('C003', 'Salinas-Chavez', '53637 Bonnie Walk Suite 961, South Adrianaport, IA', 'richard84@hotmail.com', '2545622603', 'Chelsea Hoffman'),  
  ('C004', 'Russell, Wilson and Rogers', '27907 Deborah Hill Suite 235, Abigailbury, CO', 'michael78@yahoo.com', '(995)213-6315', 'Michael Howard'),  
  ('C005', 'White Ltd', '172 Angela Crescent Apt. 306, North Laura, HI', 'jeremy56@gmail.com', '(320)185-3187', 'Nathan Weber');

select \* from \`Clients\`

\---  
    
insert into \`Campaigns\` (Campaign\_id, Name, Start\_date, End\_date, Budget, Client\_id)  
values  
  ('camp\_001', 'Campaign 1', '12-18-23', '1-10-24', 13961.03, 'C001'),  
  ('camp\_002', 'Campaign 2', '10-12-23', '11-9-23', 43804.31, 'C002'),  
  ('camp\_003', 'Campaign 3', '5-18-23', '6-4-23', 36007.47, 'C003'),  
  ('camp\_004', 'Campaign 4', '2-23-23', '3-9-23', 37425.85, 'C004'),  
  ('camp\_005', 'Campaign 5', '11-20-23', '12-11-23', 48590.34, 'C005');

select \* from \`Campaigns\`

\---  
    
insert into \`Influencers\` (Influencer\_id, Name, Social\_handle, Follower\_count, Contact\_details)  
values  
  ('inf\_001', 'Sofia Reyes',     '@sofiareyes',     1250000, 'sofia.reyes@gmail.com'),  
  ('inf\_002', 'Marcus Bell',     '@marcusbell',      875000, 'marcus.bell@outlook.com'),  
  ('inf\_003', 'Priya Nair',      '@priyanair',       540000, 'priya.nair@gmail.com'),  
  ('inf\_004', 'James Okafor',    '@jamesokafor',    2100000, 'j.okafor@protonmail.com'),  
  ('inf\_005', 'Camille Dupont',  '@camilledupont',   320000, 'camille.dupont@yahoo.com');

select \* from \`Influencers\`

\---

insert into \`Campaign\_influencer\` (Campaign\_id, Influencer\_id)  
values  
  ('camp\_001', 'inf\_001'),  \-- Lopez PLC     → Sofia Reyes  
  ('camp\_002', 'inf\_002'),  \-- Weaver & Ramos → Marcus Bell  
  ('camp\_003', 'inf\_003'),  \-- Salinas-Chavez → Priya Nair  
  ('camp\_004', 'inf\_004'),  \-- Russell & Rogers → James Okafor  
  ('camp\_005', 'inf\_005');  \-- White Ltd      → Camille Dupont

select \* from \`Campaign\_influencer\`  
\---  
    
insert into \`Payments\` (Payment\_id, Date, Amount, Payment\_type, Payment\_detail, Campaign\_id)  
values  
  ('pay\_001', '2023-12-18', 6980.52,  'Bank Transfer', 'Initial 50% deposit — Campaign 1', 'camp\_001'),  
  ('pay\_002', '2023-10-12', 43804.31, 'Credit Card',   'Full payment upfront — Campaign 2', 'camp\_002'),  
  ('pay\_003', '2023-05-18', 18003.74, 'Bank Transfer', 'First instalment — Campaign 3',    'camp\_003'),  
  ('pay\_004', '2023-02-23', 37425.85, 'Wire Transfer', 'Full payment upfront — Campaign 4', 'camp\_004'),  
  ('pay\_005', '2023-11-20', 24295.17, 'Bank Transfer', 'Initial 50% deposit — Campaign 5', 'camp\_005');

select \* from \`Payments\`

\----  
    
insert into \`Employees\` (Employee\_id, Name, Role, Address, Department, Employee\_since)  
values  
  ('emp\_001', 'Lauren Riggs',         'Sales Manager',    '412 Maple St, Austin, TX 78701',       'Sales',      '2019-03-15'),  
  ('emp\_002', 'Brandon Townsend Jr.', 'Marketing Manager','98 Lakeview Ave, Chicago, IL 60601',   'Marketing',  '2020-07-01'),  
  ('emp\_003', 'Jesus Rivera',         'HR Manager',       '305 Sunset Blvd, Miami, FL 33101',     'HR',         '2018-11-22'),  
  ('emp\_004', 'Thomas Ryan',          'Developer',        '77 Pine Road, Seattle, WA 98101',      'Logistics',  '2021-01-10'),  
  ('emp\_005', 'Melissa Haynes',       'Recruiter',        '210 Oak Avenue, Denver, CO 80201',     'Operations', '2022-05-30');

  select \* from \`Employees\`

\---

insert into Campaign\_employees (Campaign\_id, Employee\_id)  
values  
  ('camp\_001', 'emp\_001'),  \-- Campaign 1 → Lauren Riggs  
  ('camp\_002', 'emp\_002'),  \-- Campaign 2 → Brandon Townsend Jr.  
  ('camp\_003', 'emp\_003'),  \-- Campaign 3 → Jesus Rivera  
  ('camp\_004', 'emp\_004'),  \-- Campaign 4 → Thomas Ryan  
  ('camp\_005', 'emp\_005');  \-- Campaign 5 → Melissa Haynes

select \* from \`Campaign\_employees\`  
\---  
    
insert into \`Metrics\` (Metric\_id, Impressions, Clicks, Engagement, Conversion\_rate, Campaign\_id)  
values  
  ('met\_001', 23458,  1056, 7718,  2.99, 'camp\_001'),  
  ('met\_002', 92422,  1360, 8075,  0.20, 'camp\_002'),  
  ('met\_003', 45934,  1655, 2446,  1.46, 'camp\_003'),  
  ('met\_004', 30391,  2669, 1700,  0.80, 'camp\_004'),  
  ('met\_005', 52042,  4242,  191,  1.45, 'camp\_005');

select \* from \`Metrics\`

\---  
    
insert into \`Contents\` (Content\_id, Title, Description, Media\_type, Creation\_date, Campaign\_id)  
values  
  ('con\_001', 'Lopez PLC Brand Reveal',      'YouTube pre-roll ad introducing the Lopez PLC rebrand',         'Video',      '2023-12-15', 'camp\_001'),  
  ('con\_002', 'Winter Newsletter Series',    'Email sequence promoting seasonal offers for Weaver & Ramos',   'Email',      '2023-10-10', 'camp\_002'),  
  ('con\_003', 'Salinas-Chavez TikTok Drop',  '15-second TikTok clips showcasing new product line',           'Short Video', '2023-05-15', 'camp\_003'),  
  ('con\_004', 'Russell & Rogers IG Stories', 'Instagram Stories carousel highlighting service packages',      'Image',      '2023-02-20', 'camp\_004'),  
  ('con\_005', 'White Ltd Lifestyle Reel',    'Instagram Reel targeting male audience 60+ with lifestyle cues','Video',      '2023-11-18', 'camp\_005');

select \* from \`Contents\`

\---  
    
insert into \`Plataforms\` (Plataform\_id, Name, URL, Contact\_person, Contact\_phone, Contact\_email)  
values  
  ('plt\_001', 'YouTube',   'https://www.youtube.com',   'David Park',      '1-800-465-7263', 'partnerships@youtube.com'),  
  ('plt\_002', 'Email',     'https://www.mailchimp.com', 'Sarah Connors',   '1-800-315-5939', 'sarah.connors@mailchimp.com'),  
  ('plt\_003', 'TikTok',    'https://www.tiktok.com',    'Kevin Zhang',     '1-888-009-8422', 'kevin.zhang@tiktok.com'),  
  ('plt\_004', 'Instagram', 'https://www.instagram.com', 'Ana Morales',     '1-650-543-4800', 'ana.morales@instagram.com'),  
  ('plt\_005', 'Facebook',  'https://www.facebook.com',  'Chris Whitfield', '1-650-308-7300', 'chris.whitfield@facebook.com');

select \* from \`Plataforms\`

\---

insert into \`Advertisement\` (Ad\_id, Ad\_name, Type, Duration, Budget, Campaign\_id, Plataform\_id)  
values  
  ('ad\_001', 'Pre-roll Ad',    'Video',   '30 seconds', 13961.03, 'camp\_001', 'plt\_001'),  
  ('ad\_002', 'Email Blast',    'Email',   '7 days',     43804.31, 'camp\_002', 'plt\_002'),  
  ('ad\_003', 'Sponsored Post', 'Video',   '17 days',    36007.47, 'camp\_003', 'plt\_003'),  
  ('ad\_004', 'Stories Ad',     'Image',   '14 days',    37425.85, 'camp\_004', 'plt\_004'),  
  ('ad\_005', 'Feed Reel',      'Video',   '21 days',    48590.34, 'camp\_005', 'plt\_004');

select \* from \`Advertisement\`  
    
/\* Some SQL queries to check the consistency of the database:

Exercise 01:

All campaigns with their budget, sorted highest first  
Tests: basic SELECT, ORDER BY \*/

select  
  Campaign\_id,  
  Name,  
  Budget,  
  Start\_date,  
  End\_date  
from Campaigns  
order by Budget desc;

/\* Exercise 02 

All payments above $20,000  
Tests: WHERE filter, basic aggregation awareness \*/

select  
  Payment\_id,  
  Date,  
  Amount,  
  Payment\_type,  
  Campaign\_id  
from Payments  
where Amount \> 20000  
order by Amount desc;

/\* Exercise 3

Employees hired after 2020  
Tests: WHERE with date comparison \*/

select  
  Employee\_id,  
  Name,  
  Role,  
  Department,  
  Employee\_since  
from Employees  
where Employee\_since \> '2020-01-01'  
order by Employee\_since asc;

/\* Queries to test JOINS

Exercise 04

Which influencer has more campaigns?  
Tests: INNER JOIN across Campaigns and Campaign\_influencer  
\*/

select  
  ci.Influencer\_id,  
   count (ca.Campaign\_id) as number\_of\_campaigns  
  from Campaigns ca  
  inner join Campaign\_influencer ci on ca.Campaign\_id \= ci.Campaign\_id  
group by ci.influencer\_id

/\* Exercise 05  
    
Each campaign with its client name and budget  
Tests: INNER JOIN across Campaigns \+ Clients \*/

select  
  ca.Campaign\_id,  
  ca.Name          as Campaign\_name,  
  ca.Budget,  
  ca.Start\_date,  
  ca.End\_date,  
  cl.Name          as Client\_name,  
  cl.Contact\_person  
from Campaigns  ca  
join Clients    cl  on ca.Client\_id \= cl.Client\_id  
order by ca.Budget desc;

/\* Exercise 06

Which employee managed which campaign and for which client  
Tests: JOIN across Campaign\_employees \+ Employees \+ Campaigns \+ Clients\*/

select  
  em.Name            as Employee\_name,  
  em.Role,  
  em.Department,  
  ca.Name            as Campaign\_name,  
  ca.Budget,  
  ca.Start\_date,  
  ca.End\_date,  
  cl.Name            as Client\_name  
from Campaign\_employees  ce  
join Employees           em  on ce.Employee\_id  \= em.Employee\_id  
join Campaigns           ca  on ce.Campaign\_id  \= ca.Campaign\_id  
join Clients             cl  on ca.Client\_id    \= cl.Client\_id  
order by em.Name;

/\*Exercise 07 

Average Cost Per Conversion   
Logic: Budget / actual conversions (impressions × rate / 100\) \*/

select  
  ca.Campaign\_id,  
  ca.Name as Campaign\_name,  
  ca.Budget,  
  round(me.Impressions \* me.Conversion\_rate / 100, 0\) as Estimated\_conversions,  
  round(ca.Budget / nullif(me.Impressions \* me.Conversion\_rate / 100, 0), 2\)  
  as Cost\_per\_conversion  
from Campaigns ca  
join Metrics   me on ca.Campaign\_id \= me.Campaign\_id  
order by Cost\_per\_conversion asc;

/\* Exercise 08

Average Cost Per Click  
Logic: Budget / Clicks per campaign, then average across all campaigns \*/

select  
  ROUND(AVG(ca.Budget / NULLIF(me.Clicks, 0)), 2\) as Avg\_cost\_per\_click,  
  MIN(ROUND(ca.Budget / NULLIF(me.Clicks, 0), 2)) as Best\_cost\_per\_click,  
  MAX(ROUND(ca.Budget / NULLIF(me.Clicks, 0), 2)) as Worst\_cost\_per\_click  
from Campaigns ca  
join Metrics   me on ca.Campaign\_id \= me.Campaign\_id;