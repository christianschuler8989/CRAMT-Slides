<script lang="ts">
	import { Presentation, Slide, Notes, Step } from '@components'
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
		const title = "Mehrsprachige Datenaggregation für Machinenübersetzung <br>von Sprachen mit geringen Ressourcen";
		const subtitle = "(CRAMT - Cross-Lingual Resource Aggregation of<br> Low-Resource Machine Translation and Metadata)";
		const department = "Studenten Projekt"; 
		const university = "Ein Werkzeug zum Sammeln von Sprachdaten"; 
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
				<div class="text-[5vh]">
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
	<script>newChapter("Einleitung")</script>
	<Slide>
		<Layout>
			<titlebar>
				Das Team hinter CRAMT
			</titlebar>
			<mybody>
				<div class="grid" style="grid-template-columns: auto auto auto auto auto auto; mx-auto my-auto;">
					<!-- Names -->
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3.0vh]">
						Christian Schuler
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3.0vh]">
						Tramy Thi Tran
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3.0vh]">
						Deepesha Saurty
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3.0vh]">
						Anran Wang
					</div>
					<div class="flex w-[16vw] items-center justify-center gap-[10px] text-[3.0vh]">
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
						<figcaption class="text-[2vh]">
							<!-- Master student in computer science at Technical University Munich. -->
							Anran Wang, Phd Studentin, University of Saarland Graduate School; Wissenschaftliche Mitarbeiterin Max-Plank Institute, Software System, Saarbrücken.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							<!-- She is so awesome, that she did not start looking for a PhD position like most mortal beings do- the PhD position came falling out of the sky and had to apply to her first! -->
							She is super awesome, and she is super lucky to have found amazing people in Hamburg and Saarbrücken to spend time with and study with.
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
						<img src="Anran-Logos-Stacked.png" alt="saarbruecken-logo" class="h-[7vh]">
						<!-- <img src="Logo-Saarbruecken-University.png" alt="saarbruecken-logo" class="h-[7vh]"> -->
						<!-- <img src="tum-logo.png" alt="tum-logo" class="h-[7vh]"> -->
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
		<titlebar > Verarbeitung Natürlicher Sprache - ChatGPT</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="ChatGPT-01.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout>
	<Notes>
		Notes
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Verarbeitung Natürlicher Sprache - ChatGPT</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="ChatGPT-02.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout>
	<Notes>
		Notes
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Verarbeitung Natürlicher Sprache - ChatGPT</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="ChatGPT-03.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout>
	<Notes>
		Notes
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Sprachverarbeitung und Bilder - StableDiffusion</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="Domi-001.png" alt="domi01">
			</div>
			<Step>
				<div class="flex items-center justify-center">
					<img class="h-[75vh] align-middle" src="Domi-002.png" alt="domi02">
				</div>
			</Step>
			<Step>
				<div class="flex items-center justify-center">
					<img class="h-[75vh] align-middle" src="Domi-003.png" alt="domi03">
				</div>
			</Step>
			<Step>
				<div class="flex items-center justify-center">
					<img class="h-[75vh] align-middle" src="Domi-004.png" alt="domi04">
				</div>
			</Step>
		</mybody>
	</Layout>
	<Notes>
		A proud warrior holding his diploma. The warrior is clad in armor.
		Ein stolzer Krieger der sein Diplom hält. Der Krieger ist in eine Rüstung gehüllt.
	</Notes></Slide>

	<!-- <Slide><Layout>
		<titlebar > Sprachverarbeitung und Bilder - StableDiffusion</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="Domi-005.png" alt="domi01">
			</div>
			<Step>
				<div class="flex items-center justify-center">
					<img class="h-[75vh] align-middle" src="Domi-006.png" alt="domi02">
				</div>
			</Step>
		</mybody>
	</Layout>
	<Notes>
		A proud warrior holding his diploma. The warrior is clad in armor.
		Ein stolzer Krieger der sein Diplom hält. Der Krieger ist in eine Rüstung gehüllt.
	</Notes></Slide> -->



	<script>newChapter("Motivation");</script>
	<Slide><Layout>
		<titlebar > Über (Sprach-)Grenzen hinaus </titlebar>
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
		<titlebar > Schwierigkeiten beim Übersetzen </titlebar>
		<mybody class="text-[3.5vh]">
			<ul class="a" >
				<li>Das im Schottischen sehr übliche Wort "Tartle"</li>
				<ul class="a" >
					<li>Der unschöne Moment, der entsteht, während man versucht, sich an den Namen einer Person zu erinnern, der einem soeben entfallen ist.</li>
					<li>Dies gilt aber nur, wenn einem der Name dann nach einem peinlichen Moment doch noch einfällt.</li>
				</ul>
				<br>
				<li>Der Chinesische Begriff: 江湖 (jiāng hú)</li>
				<ul class="a" >
					<li>江 = river (Fluss)，湖 = lake (See)</li>
					<li>江湖 = eine Gesellschaft in welcher Bruderschaft, Kameraderie, Tapferkeit, Gerechtigkeit sehr hoch angesehen sind, und weniger Gesetze und Ordnung etabliert ist.</li>
					<li>Findet sich in Fiktion Romanen welche in antiken Zeiten (1000-1800) spielen, in denen "Kongfu" existiert und Menschen trainieren und lernen können, um große Macht zu erlangen. </li>
				</ul>
		</mybody>
	</Layout>
	<Notes>
		江湖： a society where brotherhood, comeradery, bravery, fairness is greatly valued, and less law and order established, <br>
		usually appears in fiction novels set in ancient times (1000-1800s) where kongfu is possible and people can train and learn to have great power
	</Notes></Slide>


	<Slide><Layout>
		<titlebar > Grenzen der Übersetzungsdienste (Beispiel: Google Translate) </titlebar>
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
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL01.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL02.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL03.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL04.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL05.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL06.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL07.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL08.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sprachen im Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL09.png" alt="chatGPT01">
			</div>
		</mybody>
	</Layout></Slide>

	<script> newChapter("Vorgehen"); </script>
	<Slide><Layout>
		<titlebar > Übersicht von CRAMT </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[70vw]">
				<img src="CRAMT-Tool-OverviewSimpleSlick.png" alt="ambiguities1" class="mx-auto">
				<figcaption class="text-[4.0vh]">
					Übersicht des CRAMT Werkzeuges. Nutzereingaben in blau, Hauptverarbeitungsschritte in gelb, Resultate in grün.
					<!-- Overview of the CRAMT toolkit. User inputs in blue, main processing steps in yellow and resulting artifacts in green. -->
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

	<Slide><Layout>
		<titlebar > Daten Sammeln </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[60vw]">
				<img src="CRAMT-Tool-CollectWebdata.png" alt="crawling01" class="mx-auto">
				<figcaption class="text-[4.0vh]">
					Durchforsten des Internets auf zweierlei Art.
					<!-- Overview of the CRAMT toolkit. User inputs in blue, main processing steps in yellow and resulting artifacts in green. -->
				</figcaption>
			</figure>
			<!-- <div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="CRAMT-Tool-CollectWebdata.png" alt="selenium crawling">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<Slide><Layout>
		<titlebar > Umgehen von Sprachbarrieren </titlebar>
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
		<titlebar > Extraschritte über Drittsprache </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[70vh] align-middle" src="CRAMT-Tool-TextAlignmentsGer.png" alt="tum logo">
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>

	<!-- <Slide><Layout>
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
	</Notes></Slide> -->


	<!-- <script> newChapter("Design \& Development"); </script> -->
	

	<!-- <script> newChapter("Used Tools"); </script> -->
	
	
	<!-- <Slide><Layout>
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
	</Notes></Slide> -->

	<!-- <script> newChapter("Data Quality"); </script> -->
	<script> newChapter("Menge und Qualität von Daten"); </script>

	<Slide><Layout>
		<titlebar > Über viele Wege nach Rom </titlebar>
		<mybody>
			<figure class="h-[30vh] w-[95vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentExample.png" alt="ambiguities1" class="h-[30vh]">
				<figcaption class="w-[93vw] text-[4.0vh]">
					Neue Übersetzungen über mehrere Sprachen hinweg- Angenommen, diese sind transitiv.
					<!-- Finding new word alignments by traversing multiple cross-lingual alignments and assuming these relations to be transitive. -->
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
		<titlebar > Vieldeutigkeit der Sprache - Fluch </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[90vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentLimitation.png" alt="ambiguities2" class="h-[70vh]">
				<figcaption class="w-[93vw] text-[4.0vh]">
					Das Wort "Grün" übersetzt von "Google Translate".
					<!-- The word ambiguity during translation of the German Grün into the English green resulting in additional translation candidates. -->
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
		<titlebar > Vieldeutigkeit der Sprache - Segen? </titlebar>
		<mybody>
			<figure class="h-[80vh] w-[90vw] float-left mx-auto my-auto">
				<img src="CRAMT-Tool-WordAlignmentLimitationExample.png" alt="ambiguities1" class="h-[65vh]">
				<figcaption class="w-[93vw] text-[4.0vh]">
					Um zunächst möglichst viele Daten zu bekommen, lohnt es sich teilweise, alternative Übersetzungen weiter zu verfolgen.
					<!-- Continuing on ambiguous translations (red) instead of aggregating to the most likely candidate (green) can enrich a dataset with additional labels across languages (blue). -->
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

	<Slide><Layout>
		<titlebar > Menschen als Datenquelle (Beispiel: Vietnamesisch)</titlebar> 
		<mybody>
			<div class="grid" style="grid-template-columns: 1fr 2fr 2fr ; mx-auto my-auto;">
				<div>
					<a href="http://schuler-christian.de/">
						<div class="flex items-center justify-center">
							<img class="h-[20vh] align-middle" src="title-banner.png" alt="Potato Task Link">
						</div>
					</a>
					<img class="w-[30vw] align-middle" src="mtacr-potato-login.png" alt="Potato Login">
				</div>
				
				<div>
					<Step fadeRight>
						<img class="h-[70vh] align-middle" src="mtacr-potato-nllb-mfe.png" alt="Potato Login">
					</Step>
				</div>
				<div>
					<Step fadeRight>
						<img class="h-[70vh] align-middle" src="mtacr-potato-flickr30k-vie.png" alt="Potato Login">
					</Step>
				</div>
				
				<!-- <Step fadeRight>
					<img class="h-[70vh] align-middle" src="mtacr-potato-pos.png" alt="Potato Login">
				</Step> -->
			</div>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes>
	</Slide>

	<!-- Annotation via Anchor Items  -->
	<Slide><Layout>
		<titlebar > 100 Leute - 100 Meinungen </titlebar>
		<mybody>
			<!-- <div class="flex items-center justify-center"> -->
				<figure class="h-[80vh] w-[90vw] items-center justify-center">
					<img src="CRAMT-Tool-AnnotationQuality.png" alt="quality_control" class="h-[65vh] align-middle">
					<figcaption class="w-[93vw] text-[4.0vh]">
						Um Übersetzer nicht mit Arbeit zu erschlagen, wird der Datensatz aufgeteilt.<br>
						Zudem helfen "Anker-Sätze", die Übereinstimmung zwischen den Übersetzern zu ermitteln.
					</figcaption>
				</figure>
			<!-- </div> -->
			<!-- <div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="CRAMT-Tool-AnnotationQuality.png" alt="tum logo">
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>


	<script> newChapter("Aktueller Stand"); </script>
	<Slide><Layout>
		<titlebar > Bisher Gesammelte Daten </titlebar>
		<mybody>
			<div class="grid" style="grid-template-columns: auto auto; mx-auto my-auto;">
				<img src="mtacr-2024-april.png" alt="Data Kob Mfe" class="w-[45vw] h-[40vh]">
				<Step fadeRight><img src="mtacr-2024-april-targets.png" alt="Data Kob Mfe" class="w-[45vw] h-[40vh]"></Step>
				<Step fadeDown><img src="mtacr-2024-april-noeng.png" alt="Data Kob Mfe" class="w-[45vw] h-[40vh]"></Step>
				<Step fadeDown><img src="mtacr-2024-april-all.png" alt="Data Kob Mfe" class="w-[45vw] h-[40vh]"></Step>
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>


	<!-- <script> newChapter("Future Work"); </script> -->
	<Slide><Layout>
		<titlebar > Sprachen und Daten, die auf uns warten </titlebar>
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

	<Slide><Layout>
		<titlebar > La Ende im Gelände </titlebar>
		<mybody>
			<div class="grid" style="grid-template-columns: auto; mx-auto my-auto;">
				<a href="https://github.com/christianschuler8989/CRAMT">
					<img src="CRAMT-Tool-Logo.png" alt="CRAMT Logo" class="h-[30vh]">
					<figcaption class="text-[7.0vh]">
						Weitere Information und zukünftige Entwicklungen: <br><br>
						https://github.com/christianschuler8989/CRAMT <br>
					</figcaption>
				</a>
			</div>
			
			<!-- <div>
				<a href="https://github.com/christianschuler8989/CRAMT">
					<div class="text-[3.5vh]">
						https://github.com/christianschuler8989/CRAMT
					</div>
				</a>
			</div> -->
		</mybody>
	</Layout>
	<Notes>
		These are some presenter notes that can help during the actual presentation.<br>
		They are displayed on the presenter's screen if "presenter mode" has been entered.
	</Notes></Slide>


	


	<!-- <script> newChapter("References"); </script>
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
	</Notes></Slide> -->

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
