<script lang="ts">
	import { Presentation, Slide, Notes } from '@components'
	import Layout from './layout.svelte'
</script>

<!-- Typical Errors
	
	"Uncaught TypeError: slidesInChapter[0] is undefined" and layout elements missing.
	→ This can happen if a chapter is defined but has no slides.

-->

<Presentation>	
	<script>
		// information about this presentation 
		const author = "Christian Schuler, Tramy Thi Tran, Deepesha Saurty, <br>Anran Wang, Raman Ahmad, Seid Muhie Yimam"; 
		const authorshort = "Schuler, Tran, Saurty, Wang, Ahmad, Yimam"; 
		const title = "CRAMT";
		const subtitle = "Cross-Lingual Resource Aggregation of Low-Resource<br> Machine Translation and Metadata";
		const department = "Student's Project"; 
		const university = "A Tool to collect Language Data"; 
		var currentChapterName="";
		var currentChapterNumber=0;
		var chapterNames=[];
		var toc = false;  // whether toc is to be generated
		// data structure: [chapter number, chapter name, slideID]
		var presentationData = []; 
		function newChapter(chapterName){
			currentChapterName=chapterName; 
			currentChapterNumber++;
			chapterNames.push(chapterName);
		}
		// called when new slide is created
		var page=0; 
		function newPage(){
			page++; //note that page n has index n-1
			presentationData.push({chapternr: currentChapterNumber, chapter:currentChapterName,pagenr:page});
		}
	</script>

	<!-- title page -->
	<Slide><Layout>
		<div class="m-16 flex h-[25vh] w-[90vw] bg-[var(--themecolor)] text-white items-center justify-center gap-[100px]">
			<div>
				<div class="text-[6vh]">
					<span id="mytitle"> </span>
				</div>
				<br>
				<div class="text-[4vh]">
					<span id="mysubtitle"> </span>
				</div>
			</div>
		</div>
		<br>
		<div> 
			<span id="myname"></span>
		</div>
		<br>
		<div class="text-[3vh]"> 
			<span id="myuni"></span>
		</div>
		<div class="text-[3.5vh]"> 
			<br>
			<span id="mydate"></span>
		</div>
		<br>
		<div class="flex items-center justify-center">
			<img class="h-[15vh] align-middle" src="title-logo.png" alt="tum logo">
		</div>
		<!-- fill in the data for this presentation  -->
		<script> 
			document.getElementById("mytitle").innerHTML=title;
			document.getElementById("mysubtitle").innerHTML=subtitle;
			document.getElementById("myname").innerHTML=author;
			document.getElementById("myuni").innerHTML=department+"<br>"+university;
			let today = new Date(); 
			document.getElementById("mydate").innerHTML=today.toISOString().split('T')[0]; 
		</script>
	</Layout></Slide>
	<!-- TOC -->
	<!-- <Slide>
		<script>
			toc=false; // decides whether to generate table of content page
		</script>
		<Layout>
			<toc class="flex h-full items-center justify-center gap-[100px]">
				<chpicons> </chpicons>
				<chpnames class="text-left"> </chpnames>
			</toc>
		</Layout>
	</Slide> -->
	
	<!-- intro -->
	<script>newChapter("Introduction")</script>
	<Slide>
		<Layout>
			<titlebar>
				Project Team
			</titlebar>
			<mybody>
				<div class="grid" style="grid-template-columns: auto auto auto auto auto auto; mx-auto my-auto;">
					<!-- Names -->
					<div class="flex w-[16vw] items-center justify-center gap-[10px]">
						Christian Schuler
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px]">
						Tramy Thi Tran
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px]">
						Deepesha Saurty
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px]">
						Anran Wang
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px]">
						Raman Ahmad
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3vh]">
						Seid Muhie Yimam
					</div>

					<!-- Images -->
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<a href="https://christianschuler8989.github.io/">
							<img src="Christian_Schuler_08_Energydrink.jpg" alt="christian" class="h-[40vh]">
							<figcaption class="text-[2.3vh]">
								Master student in computer science at University of Hamburg.
							</figcaption>
							<figcaption class="text-[1.3vh]">
								With a passion for languages and colors, he aims to do a PhD. <br>Additionally, he eats more pizza in one year than any of you in your lifetime!
							</figcaption>
						</a>
					</figure>
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<img src="DDLitLab-TextAsCorpusRep-Myyyy2.jpeg" alt="myy" class="h-[40vh]">
						<figcaption class="text-[2.3vh]">
							Bachelor student in something like computer science at University of Hamburg.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							She is not simply the head of our HR-department, she IS the entire department! XD #bestProjectCoordinatorInTown
						</figcaption>
					</figure>
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<img src="DDLitLab-TextAsCorpusRep-Tania2.jpg" alt="tania" class="h-[40vh]">
						<figcaption class="text-[2.3vh]">
							Bachelor student in computer science at University of Hamburg.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							By now she went down the rabbit hole of science so much, that people actually heard her say "Algorithms are fun!"
						</figcaption>
					</figure>
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<img src="Anran_Wang_01.png" alt="anran" class="h-[40vh]">
						<figcaption class="text-[2.3vh]">
							Master student in computer science at Technical University Munich.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							She is so awesome, that she did not start looking for a PhD position like most mortal beings do- the PhD position came falling out of the sky and had to apply to her first!
						</figcaption>
					</figure>
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<img src="Raman_Ahmad_01.png" alt="raman" class="h-[40vh]">
						<figcaption class="text-[2.3vh]">
							Bachelor student in computer science at Hochschule für Angewandte Wissenschaften in Hamburg.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							He is currently exploring various ways to advance the low-resource language Kurdish with a focus on the Kobani dialect.
						</figcaption>
					</figure>
					<figure class="h-[60vh] w-[15vw] float-left mx-auto my-auto">
						<a href="https://seyyaw.github.io/">
							<img src="DDLitLab-TextAsCorpusRep-Mentor.jpeg" alt="seid" class="h-[40vh]">
							<figcaption class="text-[2.3vh]">
								Technical Lead at HCDS and Research Associate at Language Technology Group in Hamburg.
							</figcaption>
						</a>
						<figcaption class="text-[1.3vh]">
							He researches low-resource languages, in particular related to the Amharic language, while he uses his spare time to mentor and supervise groups of students like noone else could! :D
						</figcaption>
					</figure>
					
					<!-- Logos -->
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="uhh-logo.png" alt="uhh-logo" class="h-[7vh]">
					</figure>
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="uhh-logo.png" alt="uhh-logo" class="h-[7vh]">
					</figure>
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="uhh-logo.png" alt="uhh-logo" class="h-[7vh]">
					</figure>
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="tum-logo.png" alt="tum-logo" class="h-[7vh]">
					</figure>
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="haw-logo.png" alt="haw-logo" class="h-[7vh]">
					</figure>
					<figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto">
						<img src="uhh-logo.png" alt="uhh-logo" class="h-[7vh]">
					</figure>
					
				</div>
			</mybody>
		</Layout>
	</Slide>

	<Slide><Layout>
		<titlebar > Beyond Languages </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="title-banner.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	

	<script>newChapter("Motivation");</script>
	<Slide><Layout>
		<titlebar > Gaps in Translation Tools </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="CRAMT-Tool-MotivationSimpleMore.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Lack of Standardization </titlebar>
		<mybody>
			<figure>
				<table>
					<tr>
						<th>Dialect Group</th>
						<th>#Var</th>
						<th>#ISO Codes</th>
						<th>#Wiki (Articles)</th>
					</tr>
					<tr>
						<td>Central Kurdish</td>
						<td>13</td>
						<td>2</td>
						<td>53,856</td>
					</tr>
					<tr>
						<td>Northern Kurdish</td>
						<td>28</td>
						<td>1</td>
						<td>75,358</td>
					</tr>
					<tr>
						<td>Southern Kurdish</td>
						<td>13</td>
						<td>1</td>
						<td>0</td>
					</tr>
					<tr>
						<td>Zazaki</td>
						<td>10</td>
						<td>3</td>
						<td>41,811</td>
					</tr>
					<tr>
						<td>Gorani</td>
						<td>13</td>
						<td>4</td>
						<td>0</td>
					</tr>
				  </table>
				<figcaption>
					Number of language varieties (#Var) and <br> corresponding ISO-Codes (#ISO) according to Glottolog [1], <br> number of wikipedia articles (#Wiki) according to Wikimedia [2].
				</figcaption>
				<p class="text-[2vh]">
					<br>
					[1] http://glottolog.org
					<br>
					[2] https://meta.wikimedia.org/wiki/List_of_Wikipedias_by_language_group
				</p>
			</figure>
			
		</mybody>
	</Layout>
	<Notes>
		Harald Hammarström, Robert Forkel, Martin Haspelmath, and Sebastian Bank. 2023. Glot- tolog 4.8. (Available online at http://glottolog.org, Accessed on 2024-03-06.).
		Wikimedia. 2024. List of Wikipedias by language group - Meta — meta.wikimedia.org. https://meta.wikimedia.org/wiki/List_of_Wikipedias_by_language_group. [Accessed 06-03-2024].
	</Notes></Slide>

	<script> newChapter("Related Work"); </script>
	<Slide><Layout>
		<titlebar > Bridging the Language Gap </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[70vh] align-middle" src="CRAMT-Tool-TextAlignmentsOverviewMulti.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Use of Pivot Languages </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[70vh] align-middle" src="CRAMT-Tool-TextAlignments.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Bilingual Lexicon Induction (TODO) </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="title-banner.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Language Ambiguities I </titlebar>
		<mybody>
			<figure class="h-[30vh] w-[95vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentExample.png" alt="ambiguities1" class="h-[30vh]">
				<figcaption class="w-[93vw]">
					Finding new word alignments by traversing multiple cross-lingual alignments and assuming these relations to be transitive.
				</figcaption>
			</figure>
			<!-- <div class="flex items-center justify-center">
				<img class="h-[30vh] w-[95vw] align-middle" src="CRAMT-Tool-WordAlignmentExample.png" alt="tum logo">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Language Ambiguities II </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[95vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentLimitation.png" alt="ambiguities2" class="h-[70vh]">
				<figcaption class="w-[93vw]">
					The word ambiguity during translation of the German Grün into the English green resulting in additional translation candidates.
				</figcaption>
			</figure>

			<!-- <div class="flex items-center justify-center">
				<img class="h-[70vh] w-[95vw] align-middle" src="CRAMT-Tool-WordAlignmentLimitation.png" alt="tum logo">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Language Ambiguities III </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[95vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentLimitationExample.png" alt="ambiguities1" class="h-[70vh]">
				<figcaption class="w-[93vw]">
					Continuing on ambiguous translations (red) instead of aggregating to the most likely candidate (green) can enrich a dataset with additional labels across languages (blue).
				</figcaption>
			</figure>

			<!-- <div class="flex items-center justify-center">
				<img class="h-[70vh] w-[95vw] align-middle" src="CRAMT-Tool-WordAlignmentLimitationExample.png" alt="tum logo">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("Design \& Development"); </script>
	<Slide><Layout>
		<titlebar > Overview of CRAMT </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[70vw]">
				<img src="CRAMT-Tool-OverviewSimpleSlick.png" alt="ambiguities1" class="mx-auto">
				<figcaption>
					Overview of the CRAMT toolkit. User inputs in blue, main processing steps in yellow and resulting artifacts in green.
				</figcaption>
			</figure>

			<!-- <div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="CRAMT-Tool-OverviewSimpleSlick.png" alt="tum logo">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("Used Tools"); </script>
	<Slide><Layout>
		<titlebar > GlotLID (TODO) </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="title-banner.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>
	
	<Slide><Layout>
		<titlebar > Potato (TODO) </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="title-banner.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("Data Quality"); </script>
	<Slide><Layout>
		<titlebar > Annotation via Anchor Items </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="CRAMT-Tool-AnnotationQuality.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("Future Work"); </script>
	<Slide><Layout>
		<titlebar > Language Data waiting to be collected </titlebar>
		<mybody>
			<div class="grid" style="grid-template-columns: auto auto auto; mx-auto my-auto;">
				<!-- Images -->
				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="Kurmanjî-wordcloud.png" alt="kurmanji" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						Kurmanji
					</figcaption>
				</figure>
				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="Morisien-wordcloud.png" alt="morisien" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						Morisien
					</figcaption>
				</figure>
				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="Vietnamese-wordcloud.png" alt="vietnamese" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						Vietnamese
					</figcaption>
				</figure>

				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="Chinese-wordcloud.png" alt="chinese" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						Chinese
					</figcaption>
				</figure>
				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="German-wordcloud.png" alt="german" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						German
					</figcaption>
				</figure>
				<figure class="h-[35vh] w-[30vw] float-left mx-auto my-auto">
					<img src="English-wordcloud.png" alt="english" class="h-[30vh]">
					<figcaption class="text-[2.3vh]">
						English
					</figcaption>
				</figure>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("Conclusion"); </script>
	<Slide><Layout>
		<titlebar > Three-fold Outcome </titlebar>
		<mybody>
			<ul class="a" >
				<li>1. Text Corpus for specific target languages aiming to provide new aligned text data.</li>
				<br>
				<li>2. Analysis of the collected and aligned data. 
					<br>Some help to get a quick idea of the data distribution such as generated word clouds,
					<br>but also reports to provide deeper insights about the data.</li>
				<br>
				<li>3. Datasheet that can represent and explain the newly created dataset and its purpose.</li>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<script> newChapter("References"); </script>
	<Slide><Layout>
		<titlebar > Poster-Related References (TODO) </titlebar>
		<mybody>
			<ul class="a" >
				<li>Ahmadi, (2020)</li>
				<li>Yu, et al., (2022)</li>
				<li>Artetxe, et al., (2022)</li>
				<li>Kreutzer, et al., (2022)</li>
				<li>Vulić, et al., (2013)</li>
				<li>Gouws, et al., (2016)</li>
				<li>Bafna, et al., (2023)</li>
				<li>Karakante, et al., (2018)</li>
				<li>Reimers, et al., (2020)</li>
				<li>de Vries, et al., (2021)</li>
				<li>Yimam, et al., (2020)</li>
				<li>Millour, et al., (2020)</li>
				<li>Lent, et al., (2022)</li>
				<li>Liu, et al., (2022)</li>
				<li>Cahyawijaya, et al., (2023)</li>
				<li>Pei, et al., (2022)</li>
				<li>Kargaran, et al., (2023)</li>
				<li>Haig, (2001)</li>
			</ul>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<!-- to mimic the latex template  -->
	<script>
		const totalSlides = document.getElementsByTagName('pagenumber').length;
		const totalChapters = chapterNames.length;
		var temp; 
		for (let i = 0; i < totalSlides; i++) {
			// one section, one slide
			document.getElementsByTagName('section')[i].setAttribute("id", "slide-"+(i+1));
			// add author name 
			document.getElementsByTagName('author')[i].innerText=authorshort;
			// add title 
			document.getElementsByTagName('mytitle')[i].innerHTML="<a href=\"#slide-1\">"+title+"</a>";
			// show slide number with total slide number
			document.getElementsByTagName("pagenumber")[i].innerHTML = (i+1)+"/"+totalSlides;
		}
		for (let i = 0; i < totalSlides; i++) {
			for (let j = 0; j < totalChapters; j++) {
				// fill in chapter names
				temp = document.querySelectorAll("table.topbar")[i]; 
				temp.getElementsByTagName("tr")[0].innerHTML += "<th data-chpcol=\"chpcol\" style=\"font-weight:normal\">"+chapterNames[j]+"</th>";
				// document.getElementsByTagName("test")[0].innerHTML="here!"; 
				// fill in dots
				let slidesInChapter = presentationData.filter(item => item.chapter == chapterNames[j]);
				let begin = slidesInChapter[0].pagenr;
				let end = slidesInChapter[slidesInChapter.length-1].pagenr;
				let circles=toCircle(begin,end);
				temp.getElementsByTagName("tr")[1].innerHTML += "<td>"+ circles +"</td>";
			}
		}
		for (let i = 0; i < totalSlides; i++) {
			// first, find out if title page and toc exist 
			let chapter0 = presentationData.filter(item => item.chapternr == 0).length;
			if (i>=chapter0){
				// then set corresponding circle to white
				let circle = document.getElementsByTagName("circle-"+(i+1))[i]; 
				circle.style.background="white";
				circle.style.border="0px";
				// also the chapter names 
				let chapterNr = presentationData.filter(item => item.pagenr == i+1)[0].chapternr;
				temp = document.getElementsByTagName("th")[(i)*(totalChapters)+chapterNr-1];
				if (temp.hasAttribute("data-chpcol")){ 
					temp.style.color="white";
				}
			}
		}
		// circles: start, start+1, . . . , end are created
		function toCircle(begin,end){
			let circles = ""; 
			for (let i=begin; i<=end; i++){
				circles+="<a href=\"#slide-" +i+ "\"><circle-" +i+ " class=\"dot\"> </circle-" +i+ "> </a>" ;
			}
			return circles;
		}
		// to create table of contents
		if (toc) {
			for (i=1; i<=chapterNames.length;i++){
				document.getElementsByTagName('chpicons')[0].innerHTML += "<div class=\"chpicon\">"+i+"</div> <br>";
				document.getElementsByTagName('chpnames')[0].innerHTML += "<div>"+chapterNames[i-1]+"</div> <br>";
			}
		}
	</script>
	
	<style>
		.chpicon{
			color: white;
			width:180%;
			background: var(--themecolor);
		}
		.dot {
			height: 15px;
			width: 15px;
			background: rgba(0,0,0,0);
			border-radius: 50%;
			border: 1.5px solid var(--themecolorlight);
			display: inline-block;
		}
		ul.a {
			list-style-type: square;
			padding-top:5vh;
		}
		ul.b {
			list-style-type: circle;
			margin-left:5vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		ul.c {
			list-style-type: disc;
			margin-left:10vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		ul{
			text-align: left;
			margin-left:20vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		titlebar{
			display:flex;
			background: rgb(242,242,242); 
			width: 100vw; 
			height: 9vh; 
			text-align: left;
			padding-left: 5vh; 
			padding-top: 2vh;
			font-size: 5vh;
		}
		mybody{
			display: flex;
			justify-content: center;
			align-items: center;
			height:79vh;
		}
		figure {
			border: 0px #cccccc solid;
			padding: 4px;
			margin: auto;
		}
		figcaption {
			background-color: rgb(242,242,242);
			color: black;
			font-style: italic;
			padding: 2px;
			text-align: center;
		}
	</style>
</Presentation>
