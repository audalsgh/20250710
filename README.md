# 13일차

## cv2 + canny + hough
1. 어제짠 코드 설명, shape를 width, height로 쪼개서 이미지의 좌표를 편하게 사용하며 roi영역을 지정했다.
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

def play_youtube_video(url, skip_frame=1):
  #유튜브 영상을 다운받아, 적당한 프레임씩 스킵해가며 재생하는 함수 만들기.
```
