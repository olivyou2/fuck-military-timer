<script lang="ts">
    let today = new Date();
    let endDate = new Date("2026-08.02T00:00:00+09:00"); // Replace with your end date
    let remainText = "";
    let militaryTime = "";

    function formatTime(ms: number): string {
        const totalSeconds = Math.floor(ms / 1000);
        const days = Math.floor(totalSeconds / (24 * 3600));
        const hours = Math.floor((totalSeconds % (24 * 3600)) / 3600);
        const minutes = Math.floor((totalSeconds % 3600) / 60);
        const seconds = totalSeconds % 60;
        const milliseconds = ms % 1000;

        return `${days}일 ${hours}시간 ${minutes}분 ${seconds}초 ${milliseconds}`;
    }

    function updateRemainingTime() {
        today = new Date();
        const remainTime = endDate.getTime() - today.getTime();

        if (remainTime <= 0) {
            remainText = "군 생활이 끝났습니다!";
            return;
        }

        const formattedTime = formatTime(remainTime);
        remainText = formattedTime;

        militaryTime = militaryTimer();
    }

    function militaryTimer() {
        let entranceDate = new Date("2025-02-03T00:00:00+09:00"); // Replace with your entrance date
        const totalDays = endDate.getTime() - entranceDate.getTime();
        const currentDays = today.getTime() - entranceDate.getTime();
        const percentage = currentDays / totalDays;

        const militaryDotHours = percentage * 24;
        const militaryHours = Math.floor(militaryDotHours);
        const militaryMinutes = Math.floor(
            (militaryDotHours - militaryHours) * 60,
        );
        const militarySeconds = Math.floor(
            ((militaryDotHours - militaryHours) * 60 - militaryMinutes) * 60,
        );
        const militaryMilliseconds = Math.floor(
            (((militaryDotHours - militaryHours) * 60 - militaryMinutes) * 60 -
                militarySeconds) *
                1000,
        );

        const militaryTime = `${militaryHours}시 ${militaryMinutes}분 ${militarySeconds}초 ${militaryMilliseconds}`;
        return militaryTime;
    }

    updateRemainingTime();
    // Update the remaining time every second
    setInterval(updateRemainingTime, 50);
</script>

<div class="desktop-1">
    <div class="title">
        <span class="t">김유성의 </span>
        <span class="b">ㄹㅇ 좆되버린 남은 군생활</span>
    </div>
    <span class="remain">{remainText} 남았습니다</span>
    <span class="remain">[국방시계] {militaryTime}</span>
</div>

<style lang="scss">
    .desktop-1 {
        width: 100vw;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 30px;
        box-sizing: border-box;
        background-color: #ffffff;
        @supports (-webkit-touch-callout: none) {
            min-height: -webkit-fill-available;
        }
        > .title {
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            flex-shrink: 0;
            position: relative;
            > .t {
                flex-shrink: 0;
                position: relative;
                font-size: 94px;
                font-weight: 600;
                color: #000000;
                font-family: Pretendard Variable;
            }

            > .b {
                flex-shrink: 0;
                position: relative;
                font-size: 60px;
                font-weight: 600;
                color: #000000;
                font-family: Pretendard Variable;
            }
        }

        > .remain {
            flex-shrink: 0;
            position: relative;
            font-size: 60px;
            font-weight: 600;
            color: #000000;
            font-family: Pretendard Variable;
        }

        > .remain {
            flex-shrink: 0;
            position: relative;
            font-size: 60px;
            font-weight: 600;
            color: #000000;
            font-family: Pretendard Variable;
        }
    }
</style>
