# CIT 386 Connection Runbook

## Purpose

This runbook explains how to connect to the course server from a Windows computer using PuTTY.

## What You Need

Before starting, make sure you have:

- A Windows computer
- PuTTY
- PuTTYgen
- The two files provided by the instructor

Create a folder for the connection files. For example:

`C:\Users\<USERNAME>\Documents\CIT386\Keys\`

Keep both files in this folder so they are easy to find later.

PuTTY is used to connect to the server. PuTTYgen is used to convert the key so PuTTY can use it.

**Important:** Never put the private key, public key, key fingerprint, or real server address in this document or GitHub.

## Convert the Key

PuTTY needs the `.pem` key converted to a `.ppk` file.

1. Open PuTTYgen.
2. Click **Load**.
3. Find and select the `.pem` file provided by the instructor.
4. After the key loads, click **Save private key**.
5. Save the new file in the same folder as the `.pem` file.
6. Make sure the new file has the `.ppk` extension.

The `.ppk` file will be used later when setting up PuTTY.

## Set Up PuTTY

1. Open PuTTY.
2. Click **Session** on the left side.
3. In **Host Name (or IP address)**, enter the server address provided by the instructor.
4. Set **Port** to `22`.
5. Make sure **SSH** is selected.
6. On the left side, go to **Connection > SSH > Auth > Credentials**.
7. Next to **Private key file for authentication**, click **Browse**.
8. Select the `.ppk` file created with PuTTYgen.
9. On the left side, go to **Connection > Data**.
10. Enter the user name provided by the instructor in **Auto-login username**.
11. Go back to **Session**.
12. Under **Saved Sessions**, enter a name such as `CIT386 Server`.
13. Click **Save**.

The connection is now saved. The next time PuTTY is opened, select `CIT386 Server`, click **Load**, and then click **Open**.

## Connect to the Server

1. Open PuTTY.
2. Select `CIT386 Server` under **Saved Sessions**.
3. Click **Load**.
4. Click **Open**.
5. The first time you connect, PuTTY may show a **host key warning**.
6. This warning means PuTTY has not connected to this server before.
7. Make sure you are connecting to the server provided by the instructor, then accept the warning.
8. PuTTY will remember the server for future connections.

A successful connection will open a terminal window and display a command prompt on the server. Once the prompt appears, the SSH connection is working.

## Successful Connection

When the connection is successful, PuTTY opens a terminal window and asks for the login name. After entering the correct login, the server authenticates using the public key.

A successful connection will then show a shell prompt. This means the SSH connection is working.

## Troubleshooting

### 1. Connection Not Supported

**Message:** The connection showed a message saying it was “not supported.”

**What it means:** In my case, the PuTTY session was not completely set up before I tried to connect.

**First thing to check:** Go back to **Session** and make sure the connection information is entered. Enter a name under **Saved Sessions**, click **Save**, then select the session and click **Load** before opening it.

## Key Handling

The private key must be kept secure. Do not upload it to GitHub or share it with anyone.

The public key can be copied to another machine if needed. The private key should not be copied or shared unless specifically authorized.

If the private key is exposed, stop using it and notify the instructor so a new key pair can be issued.

The first time you connect to the server, PuTTY may display a host key warning. This means PuTTY has not connected to this server before and does not have the server's host key saved.

Make sure you are connecting to the correct server provided by the instructor, then accept the warning. PuTTY will remember the server's host key for future connections.