# mailhub

## How it works

Let's have a team with members. Their email addresses are:

- member1@team.com
- member2@team.com
- member3@team.com

The team has a main contact address: contact@team.com and people are contacting the team on this contact address.

### An email is received from an external email address

The app is running as a background task on a server. It has imap credentials to the contact@team.com email address and it's checking everyminute if an email is received.

1. An email is received from icanhazquestions@external.com
2. mailhub reads the mail
3. it adds a custom header, let's say "X-Mailhub-Orig-Sender" with value icanhazquestions@external.com
4. it changes the Reply-to to contact@team.com
5. it resends the mail to every members of the team.

So everymember of the team is notified that icanhazquestions@external.com has sent an email to contact@team.com

### An email is received from an internal email address

Member 1 wants to reply to the email sent by icanhazquestions@external.com.

1. member1@team.com replies to the email he's just received.
2. the email is sent to contact@team.com
3. mailhub reads the mail
4. it sees it comes from a member of the team so it edits the mail
5. it sets Sender to contact@team.com
6. it takes recipient email address (icanhazquestions@external.com) from X-Mailhub-Orig-Sender and uses it.
7. it sends the mail.
8. it changes Sender to member1@team and Recipients to member2@team.com and member3@team.com and sends them the mail too.

So icanhazquestions@external.com see an answer from contact@team.com and every other members of the team know member1 has given an answer.