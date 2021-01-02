# Automated-instagram-bot
College level project for an Instagram bot
from selenium import webdriver
from time import sleep
from selenium.common.exceptions import NoSuchElementException
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import random
import string


# Change this list to your wanted comments (what you want to comment on posts)
comments = ['want to increase followers dm me but only genuine pages ',
            'Nice post- just follow me, for increasing followers   ',
            'wow very nice! want genuine followers follow me  ',
            'I like it! follow me to grow your page only for genuine pages and daily posters',
            'Super ;)-follow me guys if you want to increase followers',
            'hmmm,interesting  follow me if want to increase followers i,ll do it for free',
            ' wow want to increase followers follow me ',
            'amazing post -also check out my profile and follow me if you want more followers ',
            'awesome - follow me  for tips to increase followers',
            'i am just a bot want to increase followers follow me',
            'I like it , great post- follow my page for increasing followers ']

# This variables to keep tracking of the posts
tags=['photooftheday','love','cooking','memes','wwe']
posts = 0

# Chromedriver path. Make sure to have the same Chromedriver version as your Google Chrome browser to make it work
browser = webdriver.Chrome(
    executable_path=(r"C:\Users\Aakarshit rekhi\AppData\Local\Temp\Temp1_chromedriver_win32.zip\chromedriver.exe")) # <----- ENTER PATH HERE

browser.get(('https://www.instagram.com/accounts/login/?source=auth_switcher'))
sleep(2)


def likeAndComm():  # Likes and Comments the first 9 posts
    global posts
    for y in range(1, 4):
        for x in range(1, 4):
            post = browser.find_element_by_css_selector('div:nth-child('+str(y)+') > div:nth-child('+str(x)+') > a > div > div._9AhH0')
            browser.implicitly_wait(1)
            post.click()
            try:
                browser.find_element_by_xpath("//button[contains(text(), 'Following')]")
                present = True
            except NoSuchElementException:
                present = False
            sleep(2)
            if(present==True):
                print("click1")
                postLike = browser.find_element_by_xpath(
                    '/html/body/div[5]/div[2]/div/article/div[3]/section[1]/span[1]')
                postLike.click()
                print("Post liked")
                sleep(2)
                # comment = browser.find_element_by_xpath('/html/body/div[4]/div[2]/div/article/div[3]/section[3]/div/form').click()
                print("click2")

                try:
                    comment = browser.find_element_by_xpath(
                        '/html/body/div[5]/div[2]/div/article/div[3]/section[3]/div/form')
                    comment.click()
                    print("click 3")
                except NoSuchElementException:
                    browser.find_element_by_xpath('/html/body/div[5]/div[3]/button/div/svg/path').click()
                comment = browser.find_element_by_xpath(
                    '/html/body/div[5]/div[2]/div/article/div[3]/section[3]/div/form/textarea')
                comment.send_keys(random.choice(comments))
                print("send1-Writing comment")
                sleep(3)
                sendComment = browser.find_element_by_xpath("//button[@type='submit']")
                sendComment.click()
                print("click3-Comment-posted")
                print("searching for new post, searching...")
                sleep(4)
                posts += 1
                closePost = browser.find_element_by_xpath('/html/body/div[5]/div[3]/button/div')
                closePost.click()
                sleep(3)
            if(present==False):
                follow = browser.find_element_by_xpath('/html/body/div[5]/div[2]/div/article/header/div[2]/div[1]/div[2]')
                follow.click()
                sleep(2)
                print("click1")
                postLike = browser.find_element_by_xpath(
                '/html/body/div[5]/div[2]/div/article/div[3]/section[1]/span[1]')
                postLike.click()
                print("Post liked")
                sleep(2)
                # comment = browser.find_element_by_xpath('/html/body/div[4]/div[2]/div/article/div[3]/section[3]/div/form').click()
                print("click2")

                try:
                   comment = browser.find_element_by_xpath(
                   '/html/body/div[5]/div[2]/div/article/div[3]/section[3]/div/form')
                   comment.click()
                   print("click 3")
                except NoSuchElementException:
                    browser.find_element_by_xpath('/html/body/div[5]/div[3]/button/div/svg/path').click()
                comment = browser.find_element_by_xpath(
                '/html/body/div[5]/div[2]/div/article/div[3]/section[3]/div/form/textarea')
                comment.send_keys(random.choice(comments))
                print("send1-Writing comment")
                sleep(3)
                sendComment = browser.find_element_by_xpath("//button[@type='submit']")
                sendComment.click()
                print("click3-Comment-posted")
                print("searching for new post, searching...")
                sleep(4)
                posts += 1
                closePost = browser.find_element_by_xpath('/html/body/div[5]/div[3]/button/div')
                closePost.click()
                sleep(3)
                print('No. of posts: ' + str(posts))
    sleep(5)
    browser.get('https://www.instagram.com/explore/tags/'+random.choice(tags)+'/')
    sleep(6)
    likeAndComm()
def start():
    username = browser.find_element_by_name('username')
    username.send_keys('noob_programmer45')  # <- INSERT YOUR INSTAGRAM USERNAME HERE
    password = browser.find_element_by_name('password')
    password.send_keys('Archana@321')  # <- INSERT YOUR INSTAGRAM PASSWORD HERE
    nextButton = browser.find_element_by_xpath("//button[@type='submit']")
    nextButton.click()
    sleep(4)
    notification = browser.find_element_by_xpath("//button[contains(text(), 'Not Now')]")
    notification.click()
    browser.get('https://www.instagram.com/explore/tags/'+random.choice(tags)+'/')
    sleep(4)
    likeAndComm()  
    sleep(4)
# Start the programm
start()
