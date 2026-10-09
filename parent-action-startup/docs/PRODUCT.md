# Product Brief

## Working description

A lightweight parent–school action app that keeps important school notices, parent responses, absence notices, excuse letters, and requested submissions from getting lost.

## Primary user

A busy parent or guardian managing one or more school-age children.

The important behavior is not “parents like apps.” It is that some parents already spend meaningful time coordinating school information and may delegate this work to spouses, assistants, grandparents, or other caregivers.

## Secondary user

Teacher, adviser, school secretary, registrar, communications staff, principal, or administrator who needs to receive or track a formal parent action.

## Core problem

School-related information is fragmented across paper letters, diaries, email, Teams/Google Classroom, PDFs, portals, chat groups, screenshots, and verbal messages relayed through children.

The parent’s actual job is not reading messages. It is determining:
- which child this concerns
- whether anything is required
- what exactly must be done
- when it is due
- who owns the next step
- whether it has already been completed
- whether the school has received or accepted the response

Outbound parent workflows can be equally fragmented. Example: a child will be absent, parent informs an assistant, assistant contacts teacher, teacher acknowledges, then still requires a written excuse in a paper diary that is only seen when the child returns.

## Product promise

> Know what school needs from you. Get it done.

## Core product model

Every school-related item should resolve to:
- Child
- School
- Source
- Direction: school→parent or parent→school
- Type
- Required action
- Due date, if any
- Owner/assignee
- Current state
- Original source or record
- Timestamped history

## Core states

Parent-facing language should be simple:
- **Needs your action**
- **Waiting on school**
- **Done**

Avoid exposing complex workflow terminology unless needed.

## Parent-first wedge

The product should work before a school adopts it.

Early examples:
- parent manually creates an action from a school notice
- parent uploads/pastes a notice and later confirms extracted fields
- parent reports an absence and sends an excuse to an existing teacher/school email
- teacher receives a secure link and can acknowledge without creating an account
- parent has a history showing sent/opened/acknowledged where technically available

## School adoption path

School adoption should be progressive:
1. Receive parent-originated records.
2. Acknowledge via secure no-account links.
3. Claim/create a school workspace.
4. Import students/guardians by CSV.
5. Send structured notices in bulk.
6. Track outstanding parent actions and reminders.

No SIS/LMS integration is required for early value.

## Non-goals

See `PRODUCT_PRINCIPLES.md`. The short version: no grades, LMS, tuition, enrollment, general chat, social feed, or broad family organizer.
