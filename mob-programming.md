# Two's company, three's a mob

## Intro

Mob programming. You may have heard of it before, it's been talked about in blogs and conferences a lot but it sounds a little bit crazy right, the whole team working together on one story at a time. I mean, it's pair programming gone mad. Well lets have a look at why many teams around the world are using it and I'll share with you some of my experience. But first lets start with a little history.

## History

Around 5 years ago a development team at Hunter Industries in San Diego who were trying to improve their agile, TDD and peer programming techniques were holding a solution design workshop in a meeting room when someone remoted back into their PC and they started writing code together while talking over the problem. Eventually they were kicked out of that room but found another and continued to carry on, and in this way they continued to jump between meeting rooms for the next 2 weeks, programming as a team and everyday holding a mini retrospective and agreeing that this process was working for them and they should keep doing it.

This technique continued to gain traction until now it's practiced world wide as an effective team development process called mob programming and has a dedicated conference held in Boston.

## The mechanics

So how does it work? Simply put the whole team sit in front of a large tv or projector (or 2) and take turns passing control of the keyboard and mouse around while working together to solve the problem at hand.

#### Driver / Navigator model

This constant moving of the keyboard is key to an effective mobbing session, it follows the driver / navigator model borrowed from strong pair programming which says "For an idea to go from your head into the computer it must go through someone else's hands." In mob programming there is one driver and the rest of the team are navigators. The driver sits behind the keyboard and types code, but that's all they're supposed to do, they're discouraged from thinking how to solve the problem too much and they shouldn't be typing anything without being directed to by a navigator. The navigators discuss the idea being coded and guide the driver in creating the code. This concept is critical to engagement of the team, if the driver starts thinking too much and typing their own ideas they'll leave the others behind, but having to clearly explain to the driver what to type, the navigators have to communicate and discuss the solution out loud. Drivers are rotated on a short interval, this could be 5, 10 or 15 minutes. Shorter works better when starting out.

#### Equipment setup

A mob can be anywhere from 3 to 12 members and dedicated equipment is helpful. Meeting room hopping will quickly become tiresome and interrupt flow, so it's a good idea to setup a space with a couple of big TV screens or projectors, a single PC and any number of preferred keyboards or mice for those that like their mechanical clackers or splayed keyboards. At PageUp we'll often use this space although we find the contrast too low from the projector so we play with different IDE themes to improve the readability. 

#### Administrative tasks

During mobbing people aren't tied down for the whole day. Individuals are free to take short breaks to get coffee, go to the bathroom, check their personal emails or whatever else needs to be done. The mobbing doesn't need to stop because one person leaves.

In fact it can be helpful when working with new technology to go back to your own PC to do some research, or even better if you have a laptop handy bring that to the mobbing session. Ideally if you need to Google a solution this can be done as a mob, but there have been times we've paused the mobbing to all go away and research / spike a problem and regroup later.

If someone gets interrupted by an email, phone call or a walk up, some teams will even mob on that. Again it keeps everyone across what is being asked for and how we propose to solve it.

## The benefits

So why mob?

#### Team cohesion & redundancy

Well firstly it improves team cohesion. Mob programming necessitates that the team communicate effectively to get things done. This ensures that everyone in the team is across the current code and creates redundancy in the team. If one team member is off sick it will have little impact on the output. If a new team member is added they will be able to contribute immediately and will quickly learn from the others without distraction. 

#### Upskilling

Mobbing encourage learning. It upskills existing team members as they learn new patterns, new architectures, new ways of thinking and tips to move around the IDE quicker. I find the first thing a new mobbing team learns is each other's shortcuts. Nothing bothers a developer more than watching someone else fumble through menus when there's a snappy keyboard shortcut to complete the task.

#### Quality control

Mobbing also provides improved quality control, having 5 eyes on the code will reduce typos and 5 minds on the problem will think through the majority of the scenarios. 

My team have been using mob testing lately as a twist on sprint reviews or showcases. The idea being that as we test and explore the product together, we spot more inconsistencies and decide how to resolve them as we find them. We also think through many more scenarios than we would on our own and by regularly passing control of the keyboard everyone is kept engaged in the process.

And mobbing isn't just for developers. Product owners, business analysts and testers are encouraged to be involved in the process. They can sit with the team and be apart of the discussion going on. 

## Common fallicies

There's some comment arguments against mob programming, the first one is that productivity will drop.

Yes, the number of stories you deliver per sprint will probably decrease, but the number of stories delivered isn't an accurate measure of productivity. Delivering working, fit for purpose software is a better measure. The quality of your code will improve when the whole team is focused on it which will mean less support and rework later. Better code is also easier to build upon and means future functionality can be implemented quicker. The quality of the solution will improve, by which I mean the team will discuss and agree on the requirements and how it will work. It won't get to done and someone says that's not how I expected it to work. And difficult problems won't hold up the team as much. How often do you find yourself working alone through a problem, only to have someone else look at it with a new lens and say "what if we did it this way". It can unlock the whole issue and allow you to move forward. This process is expedited if the whole team if focused on a problem at once.

## Conclusion

So, if you're interested in mob programming, I'd highly recommend watching this youtube video which shows a mob programming team in action over a whole day. Woody Zuill, who was the agile coach from the original mob programming team also maintains a blog at mobprogramming.org which provides useful tips, and you can read the original report of the technical and findings in the PDF here. I'll try to share these slides later but you can find them online now at phdesign.com.au/presentation-mob-programming, or you can message me on Twitter. 