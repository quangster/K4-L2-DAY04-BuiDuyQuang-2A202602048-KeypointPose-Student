python tools/coco_kp_to_yolo_pose.py --coco annotations/coco_keypoints/person_keypoints_default.json --out dataset/labels/train

python tools/check_pose_labels.py --images dataset/images/train --labels dataset/labels/train

python tools/evaluate_pose_annotations.py --pred dataset/labels/train --gold gold/labels/train --images dataset/images/train --out outputs/eval_vs_gold.json