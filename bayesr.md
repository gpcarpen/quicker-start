##BayesR	Agave	Tutorial	v2

>Prerequisites
>• CyVerse/iPlant	Account


###Installing	Agave
1. Create	a	directory	to	store	your	Agave	files	and	cd into	this	directory
2. Enter:	git	clone	https://bitbucket.org/taccaci/foundation-cli.git agave-cli
3. Add	the	Agave	commands	to	your	PATH	by	entering:	
a. export	PATH=$PATH:`pwd`/agave-cli/bin
Note: This	does	not	permanently add	the	CLI	to	your	PATH.	If	you	close	that	
terminal	window,	you	will	need	to	enter	that	command	again	from	the	same	
folder.
4. Enter:	tenants-init	–tenant	3
5. Set	your	JSON	decoder	to	the	bash	implementation	by	entering:
a. export	AGAVE_JSON_PARSER=native
b. Note:	this	may	not	be	necessary	but	the	default	value	did	not	work	on	my	
machine
6. Enter:	clients-create	–N	cli_client	–D	“Test	Client”	–S
a. Enter	your	CyVerse/iPlant	credentials	when	prompted
7. Enter	auth-tokens-create	–S	
a. Enter	your	CyVerse/iPlant	credentials	when	prompted
b. Note: If	at	anytime	you	receive	a	message	regarding	an	expired	authentication	
token,	enter:	auth-tokens-refresh	-S
8. Send	me	your	CyVerse/iPlant	username(s)	so	I	can	share	my	allocation	with	you


###Uploading	To	The	Discovery	Environment
1. The	first	step	is	uploading	your	data	to	the	Discovery	Environment	by	following	this	
guide:	
https://pods.iplantcollaborative.org/wiki/display/Demanual/Uploading+and+Importing+
Data+Items+Within+the+DE. For	this	example	we	will	be	using	the	example	data	
packaged	with	the	BayesR	application.	This	data	is	included	on	the	Github	page,	
https://github.com/syntheke/bayesR,	so	we	can	use	the	“Importing	from	URL” method.
2. From	the	Discovery	Environment,	https://de.iplantcollaborative.org/de/,	click	the	Data	
button	on	the	left-hand	side.	We	are	going	to	create	a	new	folder	for	the	data	and	then	
use	the	URL	import	from	there.
3. With	the	Data	window	open,	click	on	your	username,	then	File	->	New	Folder.	I	will	be	
calling	mine	“BayesRData”
4. With	that	folder	open,	click	Upload	->	Import	from	URL.	In	a	separate	tab	or	window	
open	https://github.com/syntheke/bayesR/tree/master/example/.
5. BayesR	required	the	BED,	BIM,	and	FAM	files.	So	open	simdata.bed	in	the	example	
folder,	right	click	on	Raw,	and	copy	the	link	address.	Back	in	the	Discovery	Environment,	
paste	this	URL	into	the	first	box.	As	you	can	see,	the	end	of	the	URL	is	simdata.bed.	Copy	
this	into	the	next	two	boxes	as	well	but	change	the	.bed	to	.bim	and	.fam.	Click	import	
and	they	will	be	added	to	the	upload	queue.	That	should	be	all	that	you	need	to	do	on	
the	Discovery	Environment	at	this	point	so	you	can	close	those	windows.	
Running	BayesR	Through	Agave
1. From	your	local	machine,	create	a	folder	for	the	output	and	cd into	it.
2. Download	the	BayesR	job	skeleton	
https://www.dropbox.com/s/6t0ln19e6ihetoz/bayesR-job.json
3. Open	this	with	a	text	editor	and	edit	the	following	parameters:
a. For	jobName,	anything	will	work.	For	this	example, I	used	testBayesR
b. For	software	name,	enter	“bayesR-0.75”
c. For requested	time,	enter	“02:00:00”
d. For	inputBED	enter	
“agave://data.iplantcollaborative.org/username/folder/simdata.bed”,	replacing	
username	and	folder	with	your	own.	For	instance, mine	would	be:	
“agave://data.iplantcollaborative.org/swb5075/BayesRData/simdata.bed” and	
repeat	this	for	the	other	two	input	files	(BIM	and	FAM	files)
e. For	output,	anything	will	work.	I	will	use	“BayesRTesting”.	Save	and	close	this	
file. 																									 																
Note: You	can	copy	and	paste	this	into	a	website	like	http://jsonlint.com/ to	
ensure	that	the	JSON	file	is	formatted	correctly.
4. Using	your	local	terminal,	make	sure	you	are	in	the	same	directory	as	the	job.json	file.	
Enter: jobs-submit	–F	bayesR-job.json.	You	should	get	a	response:	“Successfully	
submitted	job	<job	ID>.	The	sample	data	takes	about	twenty	minutes	to	run	but you	can	
check	this	by	entering:	jobs-status	<job	ID> with	the	same	job	ID as	above.	Once	the	job	
is	complete,	the	response	to	this	command	will	be	“FINISHED”
5. We	now	want	to	download	the	output	data.	You	can	enter	jobs-output-list	<job	ID> to	
see	all	of	the	included	files.	For	instance	I	may	enter: jobs-output-list	
3895995830152073701-ee4acae9fffff7a7-0001-007
6. BayesR	has	six	output	files (.frq,	.gv,	.hyp,	.log,	.model,	.param	files)	which	begin	with	
the	output	parameter	from	the	job	json	file.	In	my	case,	testresults.	
7. In	order	to	download,	for	example,	the	frequency	file	enter:	jobs-output	--download	--
path	testresults.frq	3895995830152073701-ee4acae9fffff7a7-0001-007 						
Here the	--path	parameter	refers	to	which	file	you	want	to	download	and	the	long	string	
at	the	end	is	your	job	ID.
