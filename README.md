I updated part 2 based on your works

Modified:
1.	TABLE "Paper": 
	"area_name" TEXT, -->> "area_name" TEXT NOT NULL, -- Papers must be assigned to one specific research area.
	"acceptance" TEXT DEFAULT 'undecided' can be assigning any values-->>"acceptance" TEXT DEFAULT 'undecided' 
CHECK (acceptance IN ('accepted', 'rejected', 'undecided')),

2.	Add some test values to check if a paper can have > 1 authurs
   
3.	Add TRIGGER: prevent_self_review_on_writes_insert
   
4.	Add TRIGGER: update_avg_on_review_update, update_acceptance_on_review_update
