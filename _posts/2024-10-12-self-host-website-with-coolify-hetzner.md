---
layout: post
title: "Self-Host Your Website with Coolify and Hetzner"
date: 2024-11-07 15:31:00 -0500
categories: [guide]
tags: [hetzner, nextjs, coolify, self host]
---
I’ve always wanted an easy and straightforward solution to host my Next.js websites independently, away from platforms like Netlify, Vercel, or Render. Recently, I saw some people on X (formerly Twitter) talking about Coolify—and it was exactly what I was looking for! 😄

## What is Coolify?

Coolify is a free, open-source tool that allows you to easily self-host applications, databases, or services (like WordPress, Formbricks, and Grafana) without needing to manage servers yourself.

## Why Choose Hetzner?

Two words: wallet-friendly. 💸 Plus, Hetzner recently added a one-click install for Coolify, which makes setting it up a breeze like literally zero hassle.

## What You Need Before We Dive In

Make sure you have these goodies:

- A domain name (I grabbed mine from Porkbun, cause it’s fun to say 😂)

- A Hetzner Cloud server (I went with the €4.51/month option, nice and affordable)

- A Git repository for your project (GitHub or GitLab—pick your poison)


## Step 1: Setting Up Your Domain

For domains, I recommend Porkbun or Namecheap because they’re easy on the wallet and reliable. No one likes spending more than they have to, right?

## Step 2: Create a Hetzner Server

Sign in to Hetzner, and here’s what you need to do:

1. Go to **Project > New Project**, give it a name (something snazzy), and click **Add Project**.
2. Open the new project, click on **Create Resource** at the top right, and select **Servers**.

![Image](/assets/images/blog/hetzner01.png)

**Server Configuration:**

- Choose **Server Location** (note that prices vary by location).
- For the Image, go to the **Apps** tab and select **Coolify**. It’s literally that easy.
- Choose **Server Type** based on your needs.
- Set **Volume Storage** to at least 30GB. I added 40GB for a little extra wiggle room (cost me €1.76/month).

Minimum Specifications for Coolify: 2 vCPUs, 2GB RAM, and 30+ GB storage.

![Image](/assets/images/blog/hetznerdashboard.png)

Once configured, click **Create and Buy Now**.

## Step 3: Say Hello to Your Server

Hetzner will email you the IP, username, and password for your server.

Using your terminal, SSH into the server with the following command:

```bash
ssh root@<your-server-ip>
```

Replace `<your-server-ip>` with your actual IP. It will ask for the password from Hetzner, and then you'll be asked to set a new root password. Pick a good one and write it down somewhere no sticky notes, please. 😅

Coolify will automatically start installing. You’ll get a link to the dashboard, which will look something like this:

```bash
http://<your-server-ip>:8000
```
![Image](/assets/images/blog/console.png)

## Step 4: Finish Up the Coolify Setup

Follow these steps in the Coolify dashboard:

1. Open the link to your Coolify instance and complete the registration.
2. Click **Get Started** and just keep following the prompts it’s all smooth sailing.

![Image](/assets/images/blog/welcome.png)

3. When prompted, select **Localhost** as the server.

![Image](/assets/images/blog/serverstep.png)

4. Name your project and continue to **Add Resource**. Link your Git repository (using a public one for this example).

![Image](/assets/images/blog/addgit.png)

5. Click **Check Repository** to verify it.

![Image](/assets/images/blog/giturl.png)

6. Select **localhost** when asked which server to use, then proceed to **Deploy** and let Coolify build and serve your app.

![Image](/assets/images/blog/configstep.png)

If all went well, your website should be live on the link generated by Coolify.

![Image](/assets/images/blog/checksitestep.png)

## Step 5: Setting Up a Custom Domain for Coolify

Head over to your domain provider’s dashboard and tweak the DNS settings:

- Add an **A record** pointing your domain to your Hetzner server’s IP.

![Image](/assets/images/blog/dnscoolify.png)

- In Coolify, go to **Settings** and set the instance’s domain to `https://coolify.<your-domain>`. For example, if your domain is `FPLStats.live`, use `https://coolify.fplstats.live`.
- Hit **Save** and wait a few minutes for the DNS to propagate.

![Image](/assets/images/blog/customdomain.png)

Now, you can access Coolify using your custom domain, hence `https://coolify.fplstats.live` instead of `http://<your-server-ip>:8000`. No more IPs to remember!

## Step 6: Link Your App to the Domain

1. In Coolify, navigate to your project’s configuration dashboard.
2. Replace the autogenerated domain with your custom one. Make sure to include both www and non-www versions, separated by commas.

![Image](/assets/images/blog/sitecustomdomain.png)

3. Click **Save** and then **Redeploy** to apply the changes.
4. Now back in your domain’s DNS settings, add A records for both the root domain and www subdomain, pointing to your server IP.

![Image](/assets/images/blog/arecorddomain.png)
![Image](/assets/images/blog/arecorddomain2.png)

- Wait a few minutes, and boom your app should be live on your domain!

![Image](/assets/images/blog/sitepreview.png)

## Step 7: Set Up a Firewall (Because Security Matters)

For added security, set up a firewall on Hetzner:

1. Go to **Firewalls** in the Hetzner dashboard and create three inbound rules for common ports (e.g., 80, 443, and SSH).

![Image](/assets/images/blog/firewall.png)

2. Apply these rules to your server under the **Resources** tab.

![Image](/assets/images/blog/firewallapply.png)

3. Once the firewall is enabled, Coolify will only be accessible via your custom domain (`https://coolify.<your-domain>`) plus, HTTPS is all taken care of by Coolify. No need to stress over SSL certificates. 😊

## The Grand Finale

And there you have it, folks! We created a Hetzner server, set up Coolify, linked a custom domain, and configured firewall rules. Now you’re all set to self-host like a pro.

Hope this guide helped you out! If you have any questions or just wanna chat about tech stuff, hit me up on [X (Twitter)](https://twitter.com/_Marocain){:target="_blank"}.
