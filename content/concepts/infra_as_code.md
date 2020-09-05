# Infrastructure as Code

A few years ago, I read a book. That book was [Infrastructure as Code](https://amzn.to/2WjBb5c) by Kief Moris. In this book, Kief lays out a framework for defining every part of your infrastructure in text files - or as we sometimes call it, code. 

This simple philosophy of managing configuration in the same way as we do with source code revolutionized the way I approach building systems. Tools like Ansible and Terraform may seem overkill for your average media server administrator but I firmly believe they have their place. An afternoon or two learning Ansible, and that is all it takes, will save you dozens of future afternoons scratching your head wondering how you accomplished something 3 weeks, 3 months or 3 years ago.

## Make it easy

Readers frequently ask me "Which GUI do you recommend for docker?" and my answer is always `docker-compose`, which understandably confuses folks as this isn't a GUI at all (see [Management GUIs](./management_guis.md) for some GUI options). This opinion is born out of countless times rebuilding boxes both of my own and of others. 

If you've used a GUI you'll be able to relate to the tedium of clicking and typing over and over again, often having to guess at the required input and having no way other than *screenshots* to remember what you did. GUIs might feel as if they make the initial set up of a system easier but in the long run, they will bite you and are more difficult to maintain.

Put yourself in the shoes of a friendly internet stranger. The one helping you with something via a Discord chat or forum post to fix a problem with one of your containers. It's likely they'll have to ask you to share the parameters used when creating that container. At some point, they're likely to ask you for a screenshot of the web interface of your NAS software or to paste a `docker-compose` yaml snippet. The yaml snippet is easier for you to share, easier for others to read and debug and also means you can't forget the variables used when creating that container. Reverse engineering a random `docker run` command from 6 months ago or deciphering someone elses UI you've never seen before is no fun. Most of these folks are giving up their spare time to help you, so make it *easy* for them!

## Disaster Recovery

Recovering from a disaster is easier with a text file too. A backup can be as simple as copying and pasting a configuration file to a Github repository. How do you backup a GUI? Maybe it's possible, maybe not. 

We can extend this philosophy well beyond just the `docker-compose.yaml` file. What about file sharing configuration via Samba? Users? Packages installed? Bash aliases? Monitoring configurations? The list goes on.

Because I extensively use Ansible, 100% of the answers to these questions are stored in my [IronicBadger/infra](https://github.com/ironicbadger/infra) git repo. Using two or three commands it is trivial to take a vanilla Ubuntu installation to fully functional media server in only a few minutes - see [Automated Install](../installation/automated_install.md) for a demo.

## Special Snowflakes

Your server will never be "finished". It is a living, breathing manifestation of your tinkering and learning. Infrastructure as Code allows you to track changes made in real-time to the *actual code* used to deploy your *actual server*. 

Storing configuration as code is a simple concept but requires some discipline - you have to commit. 

For example, let's say you deploy a server using automation and then begin to make manual changes to it. Before long the code no longer reflects what is deployed and "configuration drift" begins to occur. Reconciliation can often be frustrating and time consuming. When adopting Infrastructure as Code, every single change should be made via a configuration management tool such as Ansible. This sounds daunting but the alternative is a special snowflake you are scared to touch. We've all had that install we're scared to format because we aren't sure quite what we'll lose if we do.

Now that we've drilled into you why Infrastructure as Code is so useful, it's time to investigate two of the primary tools used in practice. They are Ansible and Terraform.

# Ansible

![ansible-logo](../images/ansible_logo_wide.png)

Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.

# Terraform

![terraform-logo](../images/terraform_logo_wide.png)

# Which one should I use?

I get this question a lot. It's true, there is a huge overlap between Ansible and Terraform but they both *excel* in different areas. So I tend to delineate between two like this.

Terraform creates the infrastructure. Ansible configures the infrastructure.

