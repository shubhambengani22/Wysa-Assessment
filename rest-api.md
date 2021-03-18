Detailed Steps and Request, Responses and Database Schema

Step 1 - The user gives in the input for the first screen, for instance "2 to 8 weeks", and stores it in the cookie or in the localstorage,          to ensure the consistency with the user cookies, in case the user accidentally logs out or closes the application.
	     Similarly, the user has to give the input for the rest of the screens, storing the values in the cookie or localstorage.
	     We also store the value of the CurrentStep which we are in to ensure smooth transition from step n to step i (n > i). For the same           reason we use localstorage or cookies to recover the value of the previous steps.
	 
Step 2 - Now that we have all the data in the cookie, after the last screen, we can calculate the efficiency of the sleep, as well as the            playlists and other user specific paramters, and make a POST request, to store all the values in the database. 

Step 3 - After the POST request send the status code as 200, we can proceed to the home page of the application.




REQUEST BODY -

POST /api/sleep/track/data HTTP/1.1
HOST : https://wysa.com
Content-Type : application/json
Accept-Type - application/json

{
	user: {
		nickname: "john",
		sleep: {
			problem_since: 1,
			bedtime: 2021-03-17T06:27:31.278Z,
			wakeup_time: 2021-03-17T12:27:31.278Z,
			sleep_duration: 5,
			efficiency: 0.84
		}
	}
}





RESPONSE -

{
	status: 200,
	message: "The user information has been successfully stored",
	data: {
		user: {
		nickname: "john",
		id: 1,                      //Auto-increment
		sleep: {
			problem_since: 1,
			bedtime: 2021-03-17T06:27:31.278Z,
			wakeup_time: 2021-03-17T12:27:31.278Z,
			sleep_duration: 6,
			efficiency: 1.0
		},
		playlists: [
			{
				id: 1,
    			name: "playlist name",
    			duration: 1800,
    			price: 499 
			},
			{
				id: 2,
				name: "some other playlist",
				duration: 900,
				price: 199
			}, ...
		]
	}
	}
}




DATABASE SCHEMA -

User -

{
	nickname: {
		type: String,
		required: true,
		trim: true
		lowercase: true
	},
	id: {
		type: number,
		required: true,
		unique: true
	},
	problem_since: {
		type: number,
		required: true,
		trim: true
	},
	choices_for_problem_since: {
        label: {type: String},
        value: {type: number}
	},
	bedtime: {
		type: Date,
		required: true
	},
	wakeuptime: {
		type: Date,
		required: true
	},
	sleep_duration: {
		type: Date,
		required: true
	},
	playlists: {
		type: Array,
		default: []
	},
	efficiency: {
		type: number
	}
}
