# Pickleball

In this project, we will be creating a pickleball system.   Initial thoughts for design includes these files

MEMBER -- Information on people wanting to play pickleball
MemberID
FirstName
LastName
Email
Phone
Mail Address
ContactMethod (Email,Phone,Mail, preferred method first)
SkillLevel (1 to 10)
Ranking
MembershipType (Paid levels?)
Status

COURT  -- Information on the court
CourtID
CourtName
PhysicalAddress
SurfaceType
IndoorOutdoor
StandardHoursAvailable

RESERVATION -- Time slots reserved
ReservationID
MemberID
NumberOfPlayers
PlayerIDs
CourtID
ReservationDate
StartTime
CreatedDate
CreateTime
CreateMethod (Web,In Person,Automatic)
