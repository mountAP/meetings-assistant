# Meetings assistant

A service to assist you in attending your daily online meetings.

Platform: Linux _(graphical)_

## What it does

![Demo](images/demo.gif)

When it's time for a meeting,

- ###### The meetings-assistant service:

  - shows a reminder notification, and
  - opens an assistant window

- ###### The assistant window:

  - loads a meeting according to the schedule
  - opens the browser at the appropriate meeting join page (according to the id)
  - copies your name to clipboard (Hit paste and join)
  - holds the meeting password (Click to copy)
  - gives options to update your local attendance sheet

## How it works

![Overview](images/overview.svg)

## Installation

- python (get a distribution that supports `tkinter`)

  ```bash
  sudo apt-get install python3-tk
  ```

- scripts

  ```bash
  git clone https://github.com/mountAP/meetings-assistant.git
  cd meetings-assistant
  pip3 install -r requirements.txt
  ```

- service

  ```bash
  ./installer.sh --install
  ```

- check status

  ```bash
  systemctl status meetings-assistant --no-pager
  ```

## Schedule your meetings

You can modify **`data.yaml`** located in `meetings-assistant/` and add any number of meetings to the list.

**Note**

- Meeting **time** `'HH:MM'`

  - must follow 24 hour format
  - must be within single or double quotes
  - must be in 4 digit representation; preceding 0 is must for single digit hours and minutes.

  Wrong: `10:2`, `4:25`, `12:50`

  Right: `'10:02'`, `"04:25"`, `'12:50'`

- Valid values for **days**

  - a list of unquoted weekday names<br>
    `- Monday`<br>
    `- Tuesday`<br>
    `...`<br>
    `- Sunday`
  - an array of quoted weekday names `[ 'Monday', 'Tuesday', ..., 'Sunday' ]`
  - a string value `'everyday'` or `'Everyday'`

- Names, ids, passwords & days in list format need not have quotes, but you may use if you like.

```yaml
# data.yaml

attendee-name: John Doe

meetings:
  - name: Sample meeting 1
    id: 2813176975
    pswd: xxxxxx
    time: '09:00' # <---- quotes important!
    days:
      - Monday
      - Wednesday
      - Friday

  - name: Sample meeting 2
    id: 7709185120
    pswd: yyyyyyy
    time: '10:30'
    days: everyday

  - name: Sample meeting 3
    id: 7709185120
    pswd: zzzzzzz
    time: '16:15' # <---- 4:15 pm
    days: ['Tuesday', 'Thursday'] # <---- quotes important!


  #  ... add more
```

## Attendance Log

Attendance sheet **`attendance-log.csv`** will be created in `meetings-assistant/` folder after you attend/miss your first meeting. View it using any spreadsheet software.

## Test

To test if it's working, schedule a test meeting in the next 1-2 minutes and see if the Assistant Window shows up.

## Caveats

- Currently works only for Zoom users
- Meetings Assistant is intended to be used with browser. If you already have the app in your system, you may be redirected to it. Behaviour may or may not be as expected. We are working on it.

## Uninstall

Inside `meetings-assistant/` folder

```bash
./installer.sh --uninstall
```

This cleans up the service registered by meetings assistant in the system. 

