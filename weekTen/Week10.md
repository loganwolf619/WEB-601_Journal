Today we have been working on building our website and we have focusing on finishing our parts on the website we are building. 
SO far I have created the database for my website

```SQL
use apex_shutterbug;
 
 drop table if exists SupportTeam;
 drop table if exists Graphics;
 drop table if exists Users;

create table Users (
UsersID int auto_increment not null,
UsersFName varchar (100) not null,
UsersLName varchar (100) not null,
UsersEmail varchar (100) unique not null,
UsersPassword varchar (20) not null,
UsersPhone varchar (20) not null,
Primary Key (UsersID)
); 

-- use apex_shutterbug;
create table Graphics (
GraphicsID int auto_increment not null,
GraphicsType varchar (50),
GraphicsQuality varchar (50),
GraphicsTitle varchar (50),
GraphicsArtist varchar (50),
UsersID int,
Primary Key (GraphicsID),
Foreign Key (UsersID) References Users(UsersID) on delete cascade
);

create table SupportTeam (
SupportID int auto_increment not null,
FirstName varchar(50) not null,
LastName varchar(50) NOT NULL,
Email varchar (100) not null,
Message varchar (500) not null,
Date datetime not null,
UsersID int not null,
Primary Key (SupportID),
Foreign Key (UsersID) References Users (UsersID) on delete cascade
);

INSERT INTO Users (UsersFName,UsersLName,UsersEmail,UsersPassword,UsersPhone) 
VALUES 
("Miranda","Lindsey","vitae.risus.Duis@anteNunc.net","WIT54WKY4UN","02 347 1374"),
("Linus","Price","Nunc.pulvinar.arcu@urnanec.co.uk","UIF48ZWQ7QS","02 129 0223"),
("Chantale","Jenkins","auctor.velit.Aliquam@enimdiam.edu","IVB66FQJ0XQ","02 215 0011"),
("Sybil","Garner","pharetra.Quisque@magna.edu","NRI32XTS9ZW","02 033 1572"),
("Deborah","Cotton","Nullam.lobortis.quam@malesuada.co.uk","IKX25EOE7GO","02 883 7947"),
("Derek","Barry","leo.Vivamus.nibh@cubiliaCuraePhasellus.com","OGQ98GSC0KG","02 663 7105"),
("Ava","Barnett","nibh.Phasellus@aliquet.edu","MYS87OEX7EE","02 155 5432"),
("Malcolm","Vance","elementum.lorem@eratvolutpatNulla.edu","MUI09TWP9OI","02 451 0816"),
("Leigh","Cooke","habitant@magnaSuspendissetristique.com","HFL73SXR0UL","02 212 7119"),
("Clio","Mcpherson","nibh@natoquepenatibuset.co.uk","DUV22GEP6RF","02 524 1795");

INSERT INTO Graphics (GraphicsType,GraphicsQuality,GraphicsTitle,GraphicsArtist,UsersID) 
VALUES
("fames","Cum","amet","Hayden, Shay N.", 1),
("justo","sed","rutrum","Dalton, Timon F.",2),
("Phasellus","arcu.","felis,","Carr, Odessa Q.",3),
("nibh","dolor.","Sed","Sheppard, Piper D.",4),
("id,","quam.","dapibus","Levy, Pascale A.",5),
("Donec","vestibulum","purus.","Kim, Castor B.",6),
("ut,","pharetra","id","Harper, Briar W.",7),
("morbi","in,","pede","Mann, Lucas U.",8),
("Mauris","lobortis","sed","Riley, Sade M.",9),
("Vivamus","facilisis","nec","Kane, Lydia W.",10);

INSERT INTO SupportTeam (Email,FirstName,LastName,Message,Date,UsersID) 
VALUES 
("nunc.interdum@commodoat.net","Miranda","Lindsey","risus odio,","01/05/19",1),
("justo.Praesent@dui.org","Linus","Price","gravida nunc","12/05/19",2),
("rutrum.justo@faucibusutnulla.org","Chantale","Jenkins","ac","09/06/20",3),
("velit@nibh.co.uk","Sybil","Garner","ipsum.","15/04/19",4),
("Nam.porttitor@velquamdignissim.ca","Deborah","Cotton", "ornare","03/06/20",5),
("cursus.Integer@natoquepenatibus.org","Miranda","Lindsey", "malesuada fames","25/05/19",1),
("nibh.Donec.est@non.ca","Linus","Price","sapien. Aenean","29/02/20",6),
("libero@erosnonenim.net","Ava","Barnett", "nunc","20/06/20",7),
("vel.nisl@molestie.ca","Malcolm","Vance","commodo hendrerit.","06/10/20",8),
("urna@orcisem.ca","Leigh","Cooke","condimentum eget,","04/02/20",9);
```