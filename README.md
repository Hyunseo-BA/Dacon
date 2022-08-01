# Dacon
LG Aimers Competition


* 평가 산식 : Normalized RMSE (NRMSE)
def lg_nrmse(gt, preds):
    # 각 Y Feature별 NRMSE 총합
    # Y_01 ~ Y_08 까지 20% 가중치 부여
    all_nrmse = []
    for idx in range(1,15): # ignore 'ID'
        rmse = metrics.mean_squared_error(gt[:,idx], preds[:,idx], squared=False)
        nrmse = rmse/np.mean(np.abs(gt[:,idx]))
        all_nrmse.append(nrmse)
    score = 1.2 * np.sum(all_nrmse[:8]) + 1.0 * np.sum(all_nrmse[8:15])
    return score


* 평가 방식

1차 평가 : 리더보드 Private Score
2차 평가 : Private Score 상위 10팀 코드 및 PPT 제출 후 온라인 대면 평가