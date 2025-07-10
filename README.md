# 13일차

## 유튜브 동영상을 colab에 다운받아, 차선인식하는 예제 학습.
[예제 코드](0710_python_hough+youtube.ipynb)<br>

- (cv2 + canny) + hough 까지 추가된 예제 학습. 
- 챗 GPT를 이용해 맨 마지막 코드에 여러 기능을 추가해보았다.
- subplot(2, 4, 7) 까지 8개의 화면을 만들었지만, 7개만 표현했다. (+ plt.show() 직전에 plt.tight_layout()을 적어서 크기를 조절했다) 

![image](https://github.com/user-attachments/assets/a27eab8f-69e9-4e40-aca1-d141b5e4616e)

> 왼쪽 폴더에서 결과 동영상을 다운받도록 하고, 차선인식까지 해내가는 여러 단계들을 각각 plot 해서 관찰할수 있도록 함.

1. 어제짠 코드 설명, canny를 통과한 후의 이미지인 shape를 (width, height)로 쪼개서 이미지의 좌표를 편하게 사용하며 roi영역을 지정했다.
```python
# ROI 설정 (도로 영역만 분석) - 좌표는 영상에 맞게 조정 필요
def create_roi_mask(frame):
    height, width = frame.shape[:2]
    mask = np.zeros((height, width), dtype=np.uint8)

    # 도로 영역을 다각형으로 설정 (예시 - 실제 영상에 맞게 조정)
    roi_points = np.array([
        [0, height//2],           # 왼쪽 중간
        [width, height//2],       # 오른쪽 중간
        [width, height],          # 오른쪽 아래
        [0, height]               # 왼쪽 아래
    ], np.int32)

    cv2.fillPoly(mask, [roi_points], 255)
    return mask
```

2. 동영상 파일을 코랩에서 사용하려면, yt-dlp 라이브러리 설치.
```python
pip install yt-dlp

# 원하는 유튜브 영상 다운로드, 여기 링크는 교수님이 주신 주행 영상
!yt-dlp -f bestvideo+bestaudio --merge-output-format mp4 https://www.youtube.com/watch?v=tEtWnGwwCEc

def play_youtube_video(url, skip_frame=1):
  #유튜브 영상을 다운받아, 적당한 프레임씩 스킵해가며 재생하는 함수 만들기.
```
