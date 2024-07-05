This is guidance for anyone working the back-end of my portfolio site. So, mostly me. That site is built on Wagtail. 

# Getting Started

## Page Structure
It is important you follow the page structure as a lot of the code relies on what is a child of what.
```
-| Home
--| Posts Index
---| Post 1 
---| Post 2
--| Posts Tags Index Page
```
If you want to add a new Post section -- so maybe divide the blog into "Intel" and "How to", put Intel Index under Home and How to Index under home as well. 

## Setting Up Snippets
Go to wagtail admin->Snippets and add a snippet under each category

## Setting Up Nav Links
Go to wagtail admin->Settings->Navigation and add an email address and github URL. 

# FAQs
## How to Show a Page in the Top Menu?
1. Go to any top-level page. (Subpage of 'Home')
2. Click Promote.
3. Check the Show in menus checkbox.

## What is the Private Comment Field?
It is a database field that exists on every post like the other fields -- but it is not displayed outside of the admin interface. 