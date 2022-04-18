import aminofix
import concurrent.futures
import pyfiglet
from colored import fore, back, style, attr
attr(0)
print(fore.THISTLE_1 + style.BOLD)
print(pyfiglet.figlet_format(" Vicious", font="graffiti"))
print(pyfiglet.figlet_format("Advertising 2.0", font="small"))
c=aminofix.Client()
email = "ophercrist547@gmail.com"
password = "cristo_212"
c.login(email = email, password = password)
print("\nLogged in")
n=input("\033[1;32mEnter chat link :- ")
fok=c.get_from_code(n)
id=fok.objectId
comid=fok.path[1:fok.path.index("/")]
c.join_community(comId=comid)
print("\033[1;93mInside Community")
subclient=aminofix.SubClient(comId=comid,profile=c.profile)
subclient.join_chat(chatId=id)
print("\033[1;32mJoined the Chat")

k=input("enter nickname: ")
subclient.edit_profile(nickname=k)


def join_and_leave():
    try:
        subclient.leave_chat(chatId=id)
        subclient.join_chat(chatId=id)
    except BaseException:
        return

def main_process():
    while True:
        print("Joining and Leaving....")
        with concurrent.futures.ThreadPoolExecutor(max_workers=150) as executor:
            _ = [executor.submit(join_and_leave) for _ in range(100000)]



main_process()
