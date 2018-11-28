# ISOLATE ONLY BRACKTES

if {1} {
	*elementtype 5 4;
	::macroEVERYTHINGOFF
	*menufilterenable;
	*menufilterset "*";
	*displaycollectorwithfilter components "none" "" 1 1;
	
	*menufilterset "*PSO*BRACKET*";
	*displaycollectorwithfilter components "all" "" 1 1;
	*menufilterdisable;
}

# FIDN HOLE FOR ALL SOLID BRACKET

if {1} {
	*createmark elem 1 "displayed";
	*findholesinit elems 1 3 30 0 0

	*findholessolid 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0

	*findholesend
}

# CREATE BEAM FOR ALL HOLE
if {1} {
	
	*clearmarkall 1; *clearmarkall 2;
	*createmark comp 1 "^face_holes_solid";
	*isolateonlyentitybymark  1;

	*createmark elem 1 "by comp" "^face_holes_solid";
	set elemAll [hm_getmark elem 1];
	
	
	set accumList {};
	
	#*featureangleset 60;
}
	# CHECK COMP AND CREATE IF NECESSARY
		if {1} {
		# CREATE A TEMPORARY COMPONENTS
			if {[hm_entityinfo exist comp HM_MPC_BEAM -byname]} {			
				*currentcollector components HM_MPC_BEAM;
			} else {
				*createentity comps name=HM_MPC_BEAM;
			}
	}


	foreach elem $elemAll {
		if {[lsearch $accumList $elem] == -1} {
			*createmark elem 1 $elem;
			*appendmark elem 1 "by attached";
			
			set elem [hm_getmark elem 1];
			eval lappend accumList $elem;
			
			*findmark elem 1 1 1 elem 0 2;
			set attachedElem [hm_getmark elem 2];
			
			set flag 0;
			foreach elem2 $attachedElem {
				set tempConfig [hm_getvalue elem id=$elem2 dataname=config];
				if {$tempConfig == 55} {
					set flag 1;
					break;
				}
			}
			
			if {$flag == 1} { continue;}
			
			*findmark elem 2 1 1 nodes 0 1;
			
			*rigidlinkinodecalandcreate 1 0 0 123456
			
			*clearmarkall 1; *clearmarkall 2;
			
		}
	

}



if {1} {
	
	#*featureangleset 30;
	*clearmarkall 1; *clearmarkall 2;
	
	*createmark comp 1 "^face_holes_solid";
	*deletemark comp 1;
	
	*displaycollectorwithfilter components "all" "" 1 0;
	*unmaskall2;
}



