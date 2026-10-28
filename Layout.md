# Pickleball

In this project, we will be creating a pickleball system.   Initial thoughts for design includes these files

## MEMBER -- Information on people wanting to play pickleball
* MemberID
* FirstName
* LastName
* Email
* Phone
* MailAddress
* ContactMethod (Email,Phone,Mail, preferred method first)
* SkillLevel (1 to 10)
* Ranking
* MembershipType (Paid levels?)
* Status

## COURT  -- Information on the court
* CourtID
* LocationID
* CourtName
* Description
* SurfaceType
* IndoorOutdoor
* StandardHoursAvailable

## RESERVATION -- Time slots reserved
* ReservationID
* MemberID
* NumberOfPlayers
* PlayerIDs
* CourtID
* ReservationDate
* StartTime
* CreatedDate
* CreateTime
* CreateMethod (Web,In Person,Automatic)

## LOCATION -- Actual location of the courts
* LocationID
* Contact Name
* Address
* City, State Zip
* Website
