# Rolver

export class CourseDetailResolver implements Resolve<[Course,Lesson[]]> {

    constructor(private coursesService: CoursesService) {

    }

    resolve(
        route: ActivatedRouteSnapshot,
        state: RouterStateSnapshot): Observable<[Course, (Lesson[])]> {

        return this.coursesService.findCourseByUrl(route.params['id'])
            .switchMap(course => this.coursesService.findLessonsForCourse(course.id),
                (course, lessons) => <any>[course, lessons] );


    }

}
