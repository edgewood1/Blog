Chapter 3: Implementing file-based routing

	•	router will use the folders and files defined in your app/folder to construct routes.  
	•	App/events/page.js  — page for /events
	•	app/events/create/page.js — /events/create

dynamic routes
	•	app/events/[id]/page — events/5/page
	•	parameters passed to the page:

Export default function singleEvent({params}) {
return <h1> event is {params.id}</h1>/}

catch-all routes (anything else after folder name)
	•	app/events/[…id]/page.js —- /events/1/12/2024
Export default function singleEvent({params}) {
return <h1> event is {params.id.toString()}</h1>/}

Not-found route
	•	app/not-found.js

Link component

Changing the page layout
	•	app/layout
	•	shared in al subsequent routes
	•	you can add a nav var here for users. 
	•	Create component/navbar
	•	import into layout + children
	•	
to be contiued

chapter 4: server and client components

	•	all components are server by default, ie, when the browser requests a page, the server works on the code for that page, then returns the HTML output to the browser. 
	•	the JS bundle size is minimized, and the app loads faster. 

Downsides of server components: 
	•	can’t listen to browser events such as click, form submission, and changes on an input field. 
	•	You can’t use react hooks, so can’t add states and effects.  Thus, client components. 

Create cc in the component folder, and then use in server component pages. 

‘Use client’ directive
	•	transforms server to client component. 
	•	Client component allows event handlers and other interactive elemnts
	•	but then you couldn’t use server functionality.  

Best practice
	•	render everything on the server.
	•	when you need interactivity, use the directive.
	•	eg, render button in client, and the rest in server.

Watch out
	•	server can import client, but reverse is not true.

Chapter 5: server actions / deta-fetching

	•	server action: async function that’s executed on the server, 
	•	but it can be called / executed both from server and client components.
	•	created by defining the “use server” directive before a function

// server Component
export default function Home() {
	// server action
	async function create() {	
		‘use server’ 
		//…

	•	its usually organized outside the app/ folder to make it easier to manage. 
	•	App/lib/actions folder might contain action.ts
	•	this might contain a single getUser() action as follows

export async function getUser() {
  Const user data await fetch(‘site’)
Const users = await user data.json
return users
}
	•	then you call his from the server component

import {getUser} from @/lib/actions/action
export default async function Home() {
Const users = await getUser();
Return ( <div … 


Using server action from client side

	•	import server action
	•	call it from an async function
	•	you can use hooks 

When to use server actions? 
	•	api (can do this on client, but practice is not to)
	•	db
	•	process payments / validation

By using server actions the app/folder can focus on ley on routing, navigation, and components

MongoDB db setup







