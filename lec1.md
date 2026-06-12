### SECURITY FUNDAMENTALS

Security mechanism classification for a property:
1 : Prevention : Prevent issues from happening. Any precautionary measures.
2 : Detenction : Assuming an incident took place, detect them as early and as accurately as possible. 
3 : Resilience : Assumng one or multiple incidents took place, ensure the overall system securityu degrades gracefully and doesnt collapse
4 : Detterence : Measures to ensure penatlies for actors responseible for security incidents. 

Threat modeling
Thread modeiong is a process by which potential threas, such as structural vulnerabilities or the absence of appropriate safeguards can be identified and enumerated, and countermeasures prioritized. 
A threat model includes:
1) Assets
  -What are you protecting?
  -Which matter most? 
2) System goals
3) Adverasary definition - Risk assessment 

Systematic THread modeling:
Diagram-based.
Attack trees.
Checklists 
Stride 
MITRE ATT&CK
Tactics techniques and procedures 

4 Key security properties:

1) Confidentiality: (secrecy) concealing information
2) Integrty : Prevention of unauthorized changes
3) Authenticity : data and actions attributed to the correct person. 
4) Availability : Ability to use resources when needed. 

Trusted Computing base: 
Component X's TCB is all other components that must operate securely for X to be secure. 
Corollary 1: If TCB is secure, X has a chance of beng secure 
Corollary 2: If TCV misbehaves, no guarantees about X's security
Trusted != Trustworthy. 

Ideal TCB Design: 
Verifiable: implies you want TCB to be as small as . 
Tamper proof : must prevent messing with the sshd or OS executables.

Why do we care about TCB?
Securing every piece of a system is hard. 
Identifying the TCB allows us to seperate a system into a prt that must be trusted and a part that doesn't have to be. 
Can focus security efforts on the trusted piece
Caveat: determinging TCB is easier said than done. 

Which of the following is NOT in the TCB of a web browser
on your laptop?
A. The laptop’s OS
B. JavaScript the browser downloads when you visit a
website
C. The laptop’s hardware
D. The browser’s cryptographic library

Answer is B: The javascript the browser downloads, is not something that the browser can ensure that is safe, since it is entirely dependant on the website you visit. 

Key principles:
1) KISS (keep it simple, stupid)
Rule of thumb: 1-5 defects per K lines of code.
Windows 10 = 50M LoC, Linux 27 M LoC
  -In both cases essentially all in the TCB.
Smaller, simpler TCB is easier to reason about 
-e.g.: sel4(a formally verified microkerner) = 89k LoC

Fail-Safe defaults
// gemini give me a good way to explain what fail-safe defaults are. 

No security by obscurity.
Common fallacy: System is more secure if the design remains secret.
Keeping design secret is hard. 
  -someone has to build/ implement it
  -users interact with it 
  -The design may be sold to lots of people 
Findign flaws in your own design is hard. 

Complete mediation:
Every access to every object is checked by the referecne monitor. 
Easier said than done 
TOCTTOU problems (TIme to check to time of use)

Least privilege:
A user or entity should only have access to the specific data, resources and applications needed to complete a required task and nothing more. 

Seperation of duty:
Having more than one person reuquired to complete a task. 

Defense in depth:
Few defensive measures are perfect
plan for failures 
Beware risk comp[pensation. 


Systems based on ACLs (like UNIX) typically deny access
entirely if a subject is not listed on the relevant ACL. This is an
example of which principle?
A. Fail-safe defaults
B. Complete mediation
C. Separation of duty
D. Defense in depth 

A. Fail-safe defaults: The default action should be to prevent the user from acquiring the data that he is requesting, if he is authorized, only then should you branch out and give it to them
e.g.: 
  void give_data(struct user){
      if(!user->pass == pass && user->name == name){
        return NULL;
      }
      return data;
  }
  bypasses the fail safe. 








































