
Transcripts  
===========

API call to fetch a transcript
--------------------------------

I make an HTTP GET call to a URL on your site, something like:

	https://vidscripts.com/API/V1.0/transcripts/guerrilla_skepticism_on_wikipedia

Put the V1.0 in the path so that later versions of the API can be created without 
affecting users of the older API.

The "guerrilla_skepticism_on_wikipedia" portion is the unique ID of the transcript I'm asking for.


What that API call returns
--------------------------

The return from the call is a document of type "application/json" and would look something like this:

	{
		id: "guerrilla_skepticism_on_wikipedia",
		title: "Guerrilla Skepticism on Wikipedia",
		introduction: "In this video, Susan Gerbic speaks about the Guerrilla Skepticism on Wikipedia (GSoW) project. You will learn much about what happens behind the scenes of the 10th most popular website. The mission of the GSoW is to rewrite all Wikipedia pages concerning scientific skepticism, and to do so in all languages possible. They work to support the people and organizations that do the research, write the books, organize the conferences and take the heat from the anti-science and paranormal world. GSoW gives them the best possible Wikipedia pages possible, while following all the rules of Wikipedia. The GSoW has had a large impact on education around the world since 2010. The GSoW has written and rewritten hundreds of Wikipedia pages, including Spontaneous Human Combustion, Facilitated Communication, Perry DeAngelis, Genetic Literacy Project, Jerry Andrus, "Grandmother Fish" and many more.\nAffectionately called the Wikipediatrician, Susan Gerbic is the cofounder of Monterey County Skeptics and a self-proclaimed skeptical junkie. Susan is also founder of the Guerrilla Skepticism on Wikipedia (GSoW) project. She is a frequent contributor to Skeptical Inquirer (CSICOP) and Skepticality Podcast. She is the winner of the CSI In the Trenches Award from 2012, James Randi Award for Skepticism in the Public Interest 2013 and a Scientific and Technical Consultant for CSI.\nViews expressed in this video are those of the speaker and do not necessarily reflect the views of the National Capital Area Skeptics.\n",
		participants: {
			"sg": {
				first_name: "Susan",
				last_name: "Gerbic",
				image: "http://www.vidscripts.org/scripts/headshots/SusanGerbic.jpg",
				role: "Speaker"
			}
		},
		start: 1500759525, 	/* unix timestamp for Sat Jul 22 2017 14:38:45 GMT-0700 (PDT) */
							/* If date of talk is unknown, start should be 0 */
		end: 1500761621,	/* unix timestamp for Sat Jul 22 2017 15:13:41 GMT-0700 (PDT) */
							/* length in seconds can be computed by subtracting start from end */
		video: "https://www.youtube.com/watch?v=IE9rmfIPSos",
		audio: null,
		utterances: [
			{
				time: 1,	/* A count of seconds relative to 'start' */
				speaker: "sg",
				text: "So in April 2017, that would just recently passed, William Shatner, who's better known as Captain Kirk from the original Star Trek series, tweeted in support of the autism awareness month. So knowingly, or possibly unknowingly, William Shatner was unaware of the controversy of Autism Speaks. So many in the autism community say that Autism Speaks is anti-autism. Others point to promotion of past deeds they've had were.. were anti-vacs ideals."
			},
			{
				time: 46,	/* A count of seconds relative to 'start' */
				speaker: "sg",
				text: "And this was politely pointed out to William Shatner and this all happened on Twitter. So you know what happened next, right. Shatner doubled down and was attacked, and returned, and it got real ugly real quick. So David Gorski, who is a member of the skeptic community, he writes for science-based medicine, he is an oncologist and he writes under the name or Orak. But he gets a lot of flack for writing about vaccine awareness, and lots of stuff he does, but it's all usually medicine related."
			},
			/* ... */
		]
	}

The 'id' field would match the one I provide in the API URL.

The 'participant's field is an object containing participant objects, keyed by a unique ID for each speaker.
There may be only one if it's a transcript of someone's speech to an audience for example.
The 'role' field of the participant object would be used to indicate that person's role in the conversation.
This is where we would put "SE" or "IL" for an SE conversation.

The 'start' field is a Unix timestamp for the date and time when the talk started. 
If that is not known, then it should be 0.

The 'end' field is a Unix timestamp for the date and time that the talk ended.

The length of the talk (in seconds) can is simply 'end' minus 'start'.
If there 'start' was 0, then 'end' will simply represent the length of the talk.

The 'video' field is a URL for video recording of the talk, or null if not available.

The 'audio' field is a URL for audio recording of the talk, or null if not available.

The 'utterances' field is a variable length array of objects, one per utterance.
the 'time' field of the utterance object is the # of seconds after 'start' that the
utterance begins.
The 'speaker' field references the participant (from the participants object) who made the utterance.
The 'text' field is the text of the actual utterance.
Special transcript codes/escape-sequences should just be embedded into the 'text' field.


