<h1>搜索并批量爬取抖音视频</h1>

<h2>python源文件</h2>

import re
import requests
import os
import json
import time
b = input('输入搜索内容')
c = ['keyword',b]
d = tuple(c)
# print(tuple(c))
count = input('爬取视频数量（示例按0，10，20，30输入）:')
lists = ['count',count]
lists1 = tuple(lists)
headers = {
    'authority': 'www.douyin.com',<br>
    'accept': 'application/json, text/plain, */*',<br>
    'accept-language': 'zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6',
    'cookie': 'ttwid=1%7CoLl79naOz23AUw19cTH_Bvx6ZhvDZa1nxIrJ7Rvaf_s%7C1698382733%7C828e531752ddc0cb277f0c666efc685358c845d413e8a9cd716d7858ffc2ee2b; passport_csrf_token=27207dc60d910ddf965144dd354681f9; passport_csrf_token_default=27207dc60d910ddf965144dd354681f9; s_v_web_id=verify_lo8589ky_zFW1a92m_5ccK_49Pw_BbwN_O5zDdwzsYeKC; douyin.com; device_web_cpu_core=16; device_web_memory_size=8; architecture=amd64; csrf_session_id=9555db07bca75bb5c7de57c446d63b05; FORCE_LOGIN=%7B%22videoConsumedRemainSeconds%22%3A180%7D; bd_ticket_guard_client_web_domain=2; pwa2=%220%7C0%7C3%7C0%22; _tea_utm_cache_1243=undefined; MONITOR_WEB_ID=0bba6810-dc0c-4167-9552-9a984dc5b6c9; xgplayer_user_id=375862262185; volume_info=%7B%22isUserMute%22%3Afalse%2C%22isMute%22%3Atrue%2C%22volume%22%3A0.6%7D; SEARCH_RESULT_LIST_TYPE=%22single%22; dy_swidth=1536; dy_sheight=864; strategyABtestKey=%221701584246.599%22; download_guide=%223%2F20231129%2F1%22; __ac_nonce=0656c8172002ddf40d1b8; __ac_signature=_02B4Z6wo00f01tL0yjAAAIDDrHiUz1sN2MLS1M6AANHeRLzDj7PUDuONx.WBQxfmplZ9EVAeONLWrPU1FR-sp.mCkB3Nyyix82wX.5lQkAnWn7nVVYEmdjrnVA1bvF6AJ0FwjZ9YkcVe-YaV52; stream_player_status_params=%22%7B%5C%22is_auto_play%5C%22%3A0%2C%5C%22is_full_screen%5C%22%3A0%2C%5C%22is_full_webscreen%5C%22%3A0%2C%5C%22is_mute%5C%22%3A1%2C%5C%22is_speed%5C%22%3A1%2C%5C%22is_visible%5C%22%3A0%7D%22; tt_scid=p.tZd8QNfHGrUOwI7k0NpK-8ZGnW5epGz5whxYGvxoEjSP3mqyAAsh1KfZ1a6nao61d5; stream_recommend_feed_params=%22%7B%5C%22cookie_enabled%5C%22%3Atrue%2C%5C%22screen_width%5C%22%3A1536%2C%5C%22screen_height%5C%22%3A864%2C%5C%22browser_online%5C%22%3Atrue%2C%5C%22cpu_core_num%5C%22%3A16%2C%5C%22device_memory%5C%22%3A8%2C%5C%22downlink%5C%22%3A10%2C%5C%22effective_type%5C%22%3A%5C%224g%5C%22%2C%5C%22round_trip_time%5C%22%3A50%7D%22; bd_ticket_guard_client_data=eyJiZC10aWNrZXQtZ3VhcmQtdmVyc2lvbiI6MiwiYmQtdGlja2V0LWd1YXJkLWl0ZXJhdGlvbi12ZXJzaW9uIjoxLCJiZC10aWNrZXQtZ3VhcmQtcmVlLXB1YmxpYy1rZXkiOiJCSGQ1YmV1dENabmt0UDBkR01STXZnNnl1bWwxdUI0OGpkZkRMemJCbHRPMGdCaFBPTGM0d2REYXgxRVhxRCs4aWZWVStQMWp6RmpqK2U3WWhxYXBBRTg9IiwiYmQtdGlja2V0LWd1YXJkLXdlYi12ZXJzaW9uIjoxfQ%3D%3D; msToken=AT8DjGdz8L4QYf9LeTtrvlp4K-M84Y_mDRRKc7nXpFWj8nDv9VOxNU7nVKLR9niwq-qPGibzhFPXtHdiXfjtuYvYWE0GBYHB1UK2tu-qBQrQPQRtIkTHYMjp-L6rW8I=; msToken=fQaumxBSBA6Vx_rvItczc7wRkkD7zJ8yCzjTwtzf45Xxnfx6APBvgtbnnMZmGCUTvYGh2L94YvCVGqBxT6XT48HXDwezzn0frV9-6Kjox8n9NEAApRqIfuh23XOKKkk=; home_can_add_dy_2_desktop=%220%22; IsDouyinActive=true',
	'referer': 'https://www.douyin.com/search/svsdf?publish_time=0&sort_type=0&source=switch_tab&type=video',<br>
    'sec-ch-ua': '"Microsoft Edge";v="119", "Chromium";v="119", "Not?A_Brand";v="24"',
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': '"Windows"',
    'sec-fetch-dest': 'empty',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'same-origin',
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36 Edg/119.0.0.0',<br>
}

params = (
    ('device_platform', 'webapp'),
    ('aid', '6383'),
    ('channel', 'channel_pc_web'),
    ('search_channel', 'aweme_video_web'),
    ('sort_type', '0'),
    ('publish_time', '0'),
    ('keyword', '水'),
    ('search_source', 'switch_tab'),
    ('query_correct_type', '1'),
    ('is_filter_search', '0'),
    ('from_group_id', ''),
    ('offset', '0'),
    ('count', '10'),
    ('pc_client_type', '1'),
    ('version_code', '170400'),
    ('version_name', '17.4.0'),
    ('cookie_enabled', 'true'),
    ('screen_width', '1536'),
    ('screen_height', '864'),
    ('browser_language', 'zh-CN'),
    ('browser_platform', 'Win32'),
    ('browser_name', 'Edge'),
    ('browser_version', '119.0.0.0'),
    ('browser_online', 'true'),
    ('engine_name', 'Blink'),
    ('engine_version', '119.0.0.0'),
    ('os_name', 'Windows'),
    ('os_version', '10'),
    ('cpu_core_num', '16'),
    ('device_memory', '8'),
    ('platform', 'PC'),
    ('downlink', '10'),
    ('effective_type', '4g'),
    ('round_trip_time', '50'),
    ('webid', '7294498251544331814'),
    ('msToken', 'fQaumxBSBA6Vx_rvItczc7wRkkD7zJ8yCzjTwtzf45Xxnfx6APBvgtbnnMZmGCUTvYGh2L94YvCVGqBxT6XT48HXDwezzn0frV9-6Kjox8n9NEAApRqIfuh23XOKKkk='),
    ('X-Bogus', 'DFSzswVO/hiANGzZtzipSYKeej0F'),
)
params_list = list(params)
params_list[6] = d
params_list[12] = lists1
params1 = tuple(params_list)

response = requests.get('https://www.douyin.com/aweme/v1/web/search/item/', headers=headers, params=params1)
a = json.loads(response.text)
g = []
for i in a['data']:
    g.append(i['aweme_info']['share_info']['share_url']+'&from=web_code_link')


header = {
    "User-Agent": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Mobile Safari/537.36"}


def videos(surl):
    print('正在解析视频链接')
    # 获取video_id
    if len(surl) > 60:
        id = re.search(r'video/(\d.*)/', surl).group(1)
    else:<br>
        id = re.search(r'video/(\d.*)', surl).group(1)<br>
    u_id = "https://m.douyin.com/web/api/v2/aweme/iteminfo/?item_ids={}&a_bogus=".format(id)
    v_rs = requests.get(url=u_id, headers=header).json()
    y = v_rs['item_list'][0]['desc']+'#'
    titles = re.search(r'^(.*?)[#]', y).group(1)
    w = v_rs['item_list'][0]['desc']
    if not os.path.exists('video'):
        os.makedirs('video')
    req = v_rs['item_list'][0]['video']['play_addr']['uri']
    print('正在下载视频')
    v_url = "https://www.douyin.com/aweme/v1/play/?video_id={}".format(req)
    print(v_url)
    v_req = requests.get(url=v_url, headers=header,stream=True)
    with open(f'video/{titles}.mp4', 'wb') as f:
        for chunk in v_req.iter_content(chunk_size=10240):
            f.write(chunk)


def pics(surl):
    print('正在解析图片链接')
    if len(surl) > 60:
        pid = re.search(r'note/(\d.*)/', surl).group(1)
    else:
        pid = re.search(r'note/(\d.*)', surl).group(1)
    p_id = "https://m.douyin.com/web/api/v2/aweme/iteminfo/?reflow_source=reflow_page&item_ids={}&a_bogus=".format(pid)
    # print(p_id)
    p_rs = requests.get(url=p_id, headers=header).json()
    # print(p_rs)
    images = p_rs['item_list'][0]['images']
    ptitle = re.search(r'^(.*?)[；;。.#]', p_rs['item_list'][0]['desc']).group(1)
    if not os.path.exists('pic'):
        os.makedirs('pic')
    if not os.path.exists(f'pic/{ptitle}'):
        os.makedirs(f'pic/{ptitle}')
    print('正在下载图片')
    for i, im in enumerate(images):
        p_req = requests.get(url=im['url_list'][0]).content
        # print(p_req)
        with open(f'pic/{ptitle}/{str(i + 1)}.jpg', 'wb') as f:
            f.write(p_req)


if __name__ == '__main__':
    for u in range(len(g)):
        # 抖音
        surl = g[u]
        try:
            if re.search(r'/video', surl) != None:
                videos(surl)
                time.sleep(0.5)
            elif re.search(r'/note', surl) != None:
                pics(surl)
                time.sleep(0.5)
            else:
                quit = input('解析失败，按回车键退出程序。')
        except:
            print('链接分析失败')
